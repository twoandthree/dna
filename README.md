# dnecho "# dna" >> README.md
#Steven Johnston
#04/04/2018
#Project 8

#This program reads in a file, and outputs information regarding neuclotides.
#The program utilizes for loops, and stores certain data into variables.
#It outputs the amount of nucleotides in a "Region Name", the amount of times
#they occurr, and their total mass. 


def nuc_counts(actual_nucleotides, output_file):

        a = 0
        c = 0
        g = 0
        t = 0
        j = 0

        A = 135.128
        C = 111.103
        G = 151.128
        T = 125.107
        J = 100.000
        
        for i in range(len(actual_nucleotides)):
            if actual_nucleotides[i] == 'A':
                a += 1

            elif actual_nucleotides[i] == 'C':
                c += 1

            elif actual_nucleotides[i] == 'G':
                g += 1
                
            elif actual_nucleotides[i] == 'T':
                t += 1
                
            elif actual_nucleotides[i] == '-':
                j += 1

        nuc_counts = [a, c, g, t]

###

        mass_math_total = (a * A) + (c * C) + (g * G) + (t * T) + (j * J)        
        mass_percentage = [round(a * A / mass_math_total * 100, 1),
                           round(c * C / mass_math_total * 100, 1),
                           round(g * G / mass_math_total * 100, 1),
                           round(t * T / mass_math_total * 100, 1),
                           round(j * J / mass_math_total * 100, 1)]

        output_file.write("Nuc. Counts: " + str(nuc_counts) + "\n")
        output_file.write("Total Mass%:" + str(mass_percentage) + "of" +
                          str(round(mass_math_total, 1)) + "\n")
        output_file.write("\n")       


            
def main():
    print("This program reports information about DNA")
    print("nucleotide sequences that may encode proteins")
    user_input_file = str(input("Input file name? "))
    user_output_file = str(input("Output file name? "))

    upper_sorted_nucleotides = []

    file = open(user_input_file)
    output_file = open(user_output_file, "w")
    dna_data = file.readlines()
    for i in range(0, len(dna_data), 2):
        sorted_dna = dna_data[i].strip()
        sorted_nucleotides = dna_data[i + 1].strip().upper()
        upper_sorted_nucleotides = sorted_nucleotides.upper()
        output_file.write("Region name: " + str(sorted_dna) + "\n")
        output_file.write("Neucleotides: " + str(sorted_nucleotides) + "\n")
            
    nuc_counts(upper_sorted_nucleotides, output_file)
    
main()




#Steven Johnston
#04/20/2018
#CSC110
#Section D

#This program simulates a fire utilizing a list of lists to output the
#the simulation. This program utilizes drawing panel to illustrate graphically
#how a fire might spread according to the progagation percentage. #This program


from DrawingPanel import*
import random
SIZE = 75

#This function reads in the text file given, and turns it into a list of lists
#so to be iterated through, and ultimately simulate the fire.
def fire(map_lines):
    grid = []
    for line in map_lines:
        clean_line = line.strip().split()
        grid.append(clean_line)
    return grid

#This function takes in the previous list as a parameter, and utilizes
#conditionals to determine how, and if the fire will spread. It also copies
#the old list into a new one so to output the fire correctly. The function looks
#for '1's, and checks for the values that are north, south, east, and west of
#the value at [i][j] respectively. A random int, and the propagation percentage
#determine whether the fire will spread. All '2's become '0's on the next turn
#since they burn up in correlation to the spec. 
def fire_spread(grid_actual_old):
    grid_actual = grid_actual_old.copy()
    for i in range(0, len(grid_actual)):
        for j in range(0, len(grid_actual[i])):
            if grid_actual[i][j] == '1':
                propagation = (random.randint(0, 100))
                if grid_actual[i - 1][j] == '2':
                    if propagation < SIZE:
                        grid_actual[i][j] = '2'
                            
                elif grid_actual[i + 1][j] == '2':
                    if propagation < SIZE:
                        grid_actual[i][j] = '2'
                                
                elif grid_actual[i][j - 1] == '2':
                    if propagation < SIZE:
                        grid_actual[i][j] = '2'
                                
                elif grid_actual[i][j + 1] == '2':
                    if propagation < SIZE:
                        grid_actual[i][j] = '2'
                                                       
            elif grid_actual[i][j] == '2':
                    grid_actual[i][j] = '0'
        
    return grid_actual

#This function sorts through the grid checking for '2's. When it no longer finds
#any '2's in the list, it will return False, and stop the simulation.
def still_burning(lis):
    for i in range(len(lis)):
        for j in range(len(lis[i])):
            if lis[i][j] == '2':
                return True
    return False

#This function takes all the ouput, and draws it on the drawing panel. It draws
#it according to the spec. The panel is draw by the length of the grid times 10
#as well as the squares.
def draw_fire(p, grid_actual):
    p.sleep(1000)
    for i in range(len(grid_actual)):
        for j in range(len(grid_actual[i])):
            if grid_actual[i][j] == '0':
                p.fill_rect(j * 10, i * 10, 10, 10, "grey")
            elif grid_actual[i][j] == '1':
                p.fill_rect(j * 10, i * 10, 10, 10, "green")
            elif grid_actual[i][j] == '2':
                p.fill_rect(j * 10, i * 10, 10, 10, "red")
                

def main(): 
    one_text = input("File name? ")
    file = open(one_text)
    lines = file.readlines()    
    actual_grid = fire(lines)
    p = DrawingPanel(len(actual_grid) * 10, len(actual_grid[0]) * 10)

    while still_burning(actual_grid):
        grid_actual = fire_spread(actual_grid)
        draw_fire(p, grid_actual)

    
main()



