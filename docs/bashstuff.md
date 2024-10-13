#Bash ALIASES
<pre>
  <span style="color: #3366ff;">#alias ports='ss -lt'</span>
  <span style="color: #3366ff;">#alias ports1='netstat -pantu'</span>
  <span style="color: #3366ff;">alias netsettings='nmcli'</span>
  <span style="color: #3366ff;">alias diskdata='duf'</span>
  <span style="color: #3366ff;">alias foldershow='ncdu'</span>
  <span style="color: #3366ff;">alias LSBlk='lsblk -o +UUID,PARTUUID'</span>
  <span style="color: #3366ff;">alias LSBlk1='lsblk -o +UUID,FSTYPE,PARTUUID'</span>
  <span style="color: #3366ff;">alias LSBLK='lsblk -o \"NAME,MAJ:MIN,RM,SIZE,RO,FSTYPE,MOUNTPOINT,UUID\"'</span>
  <span style="color: #3366ff;">alias diskbyid='ls -lF /dev/disk/by-id'</span>
  <span style="color: #3366ff;">alias disku='duf'</span>
  <span style="color: #3366ff;">alias rootcompare='sudo QT_GRAPHICSSYSTEM=native bcompare'</span>
  <span style="color: #3366ff;">alias showdisks='sudo lshw -short -C disk'</span>
  <span style="color: #3366ff;">alias minecraft='~/.minecraft/launcher/minecraft-launcher'</span>
  <span style="color: #3366ff;">alias lsblk2='lsblk -o type,name,label,partlabel,size,fstype,model,serial,wwn,uuid'</span>
  <span style="color: #3366ff;">#alias youtube='echo yt-dlp <url>'</span>
  <span style="color: #3366ff;">alias ssh='ssh -XC'</span>
</pre>

#Bash ARRAYS:
Are you finding it challenging to determine the length of an array in Bash? You’re not alone. Many developers find themselves puzzled when it comes to handling arrays in Bash, but we’re here to help.

Think of Bash’s array length command as a measuring tape – allowing us to quickly and accurately gauge the size of our arrays, providing a versatile and handy tool for various tasks.

In this guide, we’ll walk you through the process of determining the length of an array in Bash, from the basics to more advanced techniques. We’ll cover everything from the simple use of the ${#array[@]} syntax to more complex scenarios, as well as alternative approaches.

Let’s get started!
TL;DR: How Do I Find the Length of an Array in Bash?

    To find the length of an array in Bash, you can use the ${#array[@]} syntax. This command will return the number of elements in the array.

Here’s a simple example:

array=("apple" "banana" "cherry")
echo "${#array[@]}"

# Output:
# 3

Bash
In this example, we’ve created an array with three elements: ‘apple’, ‘banana’, and ‘cherry’. The ${#array[@]} syntax is used to find the length of the array, which in this case is 3.

Bash Array Length: The Basics

Before we dive into complex scenarios, let’s start with the basics of finding the length of an array in Bash. The syntax for finding the length of an array is ${#array[@]}.

Let’s look at a simple example:

fruits=("apple" "banana" "orange" "grape" "pineapple")
echo "${#fruits[@]}"

# Output:
# 5

Bash

In this example, we’ve created an array named ‘fruits’ with five elements. We then use the ${#fruits[@]} syntax to find the length of the array, which returns 5, as there are five elements in the array.

This basic usage of the ${#array[@]} syntax is the foundation for finding the length of an array in Bash. As you become more comfortable with this concept, you can start to explore more advanced scenarios.

Intermediate Bash: Length of Multi-Dimensional Arrays and Empty Elements

As you gain more experience with Bash, you’ll likely encounter more complex scenarios. For example, you may need to determine the length of a multi-dimensional array or handle arrays with empty elements. Let’s take a closer look at these situations.
Multi-Dimensional Arrays

In Bash, multi-dimensional arrays aren’t supported directly. However, you can simulate them using one-dimensional arrays. Here’s an example:

matrix=("1 2 3" "4 5 6" "7 8 9")
for row in "${matrix[@]}"; do
    set -- $row
    echo "${#*[@]}"
done

# Output:
# 3
# 3
# 3

Bash

In this example, we’ve created a simulated 3×3 matrix. Each element of the ‘matrix’ array is a string representing a row of the matrix. The set -- $row command splits the string into separate elements, and ${#*[@]} gives the number of elements in each row, effectively giving us the ‘length’ of each dimension.
Handling Empty Elements

Bash considers an empty string as a valid array element. Therefore, it contributes to the length of the array. Let’s see this in action:

array=("apple" "" "cherry")
echo "${#array[@]}"

# Output:
# 3

Bash

In this example, ‘apple’, an empty string, and ‘cherry’ are the elements of the array. Even though the second element is an empty string, Bash counts it as a valid element, so the length of the array is 3.

These are some of the more complex scenarios you might encounter when finding the length of an array in Bash. Understanding these concepts will help you handle arrays more effectively in your scripts.
Alternative Methods: Bash Array Length

While the ${#array[@]} syntax is the most straightforward way to determine the length of an array in Bash, there are alternative approaches you can use. Let’s explore some of these methods, their benefits, drawbacks, and when to use them.
Using a Loop

One way to find the length of an array is by using a loop to iterate over the array elements. Here’s an example:

fruits=("apple" "banana" "orange" "grape" "pineapple")
length=0
for fruit in "${fruits[@]}"; do
    length=$((length+1))
done
echo $length

# Output:
# 5

Bash

In this example, we initialize a counter (length) to zero. Then, for each element in the array, we increment the counter by one. After the loop, length holds the number of elements in the array.

This method provides more control and can be useful in scenarios where you want to perform additional operations on each element. However, it’s more verbose and less efficient than the ${#array[@]} syntax.
Using External Commands

You can also use external commands like awk or wc to find the length of an array. Here’s an example using printf and wc:

fruits=("apple" "banana" "orange" "grape" "pineapple")
length=$(printf '%s\n' "${fruits[@]}" | wc -l)
echo $length

# Output:
# 5

Bash

In this example, we use printf to print each element on a new line, then pipe the output to wc -l to count the number of lines. This gives us the number of elements in the array.

This method can handle large arrays and complex string manipulations, but it’s slower and less readable than the ${#array[@]} syntax. It also depends on external commands, which may not be available in all environments.

In conclusion, while the ${#array[@]} syntax is generally the best way to find the length of an array in Bash, understanding these alternative methods can broaden your scripting skills and help you tackle a wider range of problems.
Troubleshooting Bash Array Length

While finding the length of an array in Bash is generally straightforward, there are some common issues that you might encounter. In this section, we’ll discuss these potential problems and provide solutions to overcome them.
Special Characters in Array Elements

Bash treats some characters as special, which can cause unexpected behavior when they’re included in array elements. Let’s look at an example:

array=("apple" "banana \n cherry")
echo "${#array[@]}"

# Output:
# 2

Bash

In this example, the array has two elements: ‘apple’ and ‘banana \n cherry’. Despite the newline character (\n) in the second element, Bash still counts it as a single element, so the length of the array is 2.

To handle special characters in array elements, you can use quotes to treat the entire string as a single element.
Large Arrays

When dealing with large arrays, the ${#array[@]} syntax can become slow. In these cases, you might want to consider using an external command like wc, as discussed in the ‘Alternative Approaches’ section.

Here’s a code example for handling large arrays:

large_array=($(seq 1 10000))
length=$(printf '%s\n' "${large_array[@]}" | wc -l)
echo $length

# Output:
# 10000

Bash

In this example, we’ve created a large array with 10,000 elements using the seq command. We then use printf and wc to find the length of the array.

Remember, while this method can handle large arrays, it’s slower and less readable than the ${#array[@]} syntax. It also depends on external commands, which may not be available in all environments.

By understanding these common issues and their solutions, you can handle arrays more effectively in your Bash scripts.

Understanding Arrays in Bash

Before we delve deeper into the nuances of determining the length of arrays in Bash, it’s crucial to understand what arrays are and how they function in Bash.
What is an Array?

An array is a data structure that stores a collection of elements. These elements, also known as values, are stored in a specific order and can be accessed by their index, which is their position in the array.

In Bash, arrays are zero-indexed, meaning the first element is at index 0, the second element is at index 1, and so on.

Here’s a simple example of an array in Bash:

fruits=("apple" "banana" "cherry")
echo "${fruits[0]}"

# Output:
# apple

Bash

In this example, ‘apple’, ‘banana’, and ‘cherry’ are the elements of the array. The command echo "${fruits[0]}" prints the first element of the array, which is ‘apple’.
Manipulating Arrays in Bash

Bash provides various commands to manipulate arrays, such as adding elements, removing elements, and finding the length of an array.

For instance, to add an element to an array, you can use the following syntax:

fruits=("apple" "banana" "cherry")
fruits+=("orange")
echo "${fruits[@]}"

# Output:
# apple banana cherry orange

Bash

In this example, we’ve added ‘orange’ to the ‘fruits’ array. The += operator is used to append elements to an array in Bash.
Data Structures in Bash

In addition to arrays, Bash supports other data structures like strings and associative arrays. While strings are simple data structures that hold a sequence of characters, associative arrays (also known as hash maps) are more complex and hold pairs of keys and values.

Understanding these fundamental concepts about arrays and data structures in Bash is crucial for effective scripting. With this knowledge, you can better understand how to determine and manipulate the length of an array in Bash.
The Power of Arrays in Bash Scripting

Arrays are incredibly versatile and powerful tools in Bash scripting. They are fundamental to a multitude of tasks and operations, making them an indispensable part of any Bash programmer’s toolkit.
Arrays in File Handling

Arrays can be used to handle files and directories in Bash. For instance, you can store the list of files in a directory in an array and perform operations on each file. Here’s an example:

files=(/path/to/directory/*)
for file in "${files[@]}"; do
    echo "Processing $file"
done

# Output:
# Processing /path/to/directory/file1
# Processing /path/to/directory/file2
# ...

Bash

In this example, we’ve stored all the files in a directory in an array. We then iterate over the array and print a message for each file.
Arrays in Data Processing

Arrays also play a crucial role in data processing tasks in Bash. They can be used to store and manipulate data, making it easier to perform complex operations. For instance, you can use an array to store the lines of a CSV file and process each line. Here’s an example:

IFS=$'
' lines=($(cat data.csv))
for line in "${lines[@]}"; do
    echo "Processing $line"
done

# Output:
# Processing line1
# Processing line2
# ...

Bash
In this example, we’ve read a CSV file line by line into an array using the cat command. We then iterate over the array and process each line.

Source: <br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;https://ioflood.com/blog/bash-length-of-array/<br />
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;https://www.geeksforgeeks.org/bash-scripting-array/

#Bash FUNCTIONS:
  <span style="color: #000000;">
    <span style="color: #3366ff;">thefunctionname()</span> {<br />
    <span style="color: #3366ff;">if</span> [ $# -eq 0 ]<br />
    <span style="color: #3366ff;">then</span><br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Usage: thefunctionname someargument"<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Example: Blah blah blah."<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "     thefunctionname someargument"<br />
    <span style="color: #3366ff;">else</span><br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Running thefunctionname... " $1<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;thefunctionname $1<br />
    <span style="color: #3366ff;">fi</span><br />
    }<br />
	</span>
    
  <span style="color: #000000;">
    A function using if/case:<br >
    <span style="color: #3366ff;">anotherfunction()</span> {<br />
    <span style="color: #3366ff;">if</span> [ $# -eq 0 ]<br />
    <span style="color: #3366ff;">then</span><br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "anotherfunction someargument"<br />
    <span style="color: #3366ff;">else</span><br />
    <span style="color: #3366ff;">case</span> $1 in<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;argument1)<br />
            	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;do some work<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;argument2)<br />
              &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;do some work<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;<br />
            *)<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;message="Default message if no argument is supplied."<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo $message<br />
            &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;;;<br />
    <span style="color: #3366ff;">esac</span><br />
    <span style="color: #3366ff;">fi</span><br />
    }<br />
	</span>

#STAT command:
   <span style="color: #3366ff;">stat -c "%a %n %C" filename.txt </span><br />

#The following examples prints numbers from 1 to 10 using the for and while loops
   <span style="color: #3366ff;">echo "for(i=1;i<=10;i++) {i;}" | bc </span><br />
   <span style="color: #3366ff;">echo "i=1; while(i<=10) {i; i+=1}" | bc </span><br />
 

