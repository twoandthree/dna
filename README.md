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


