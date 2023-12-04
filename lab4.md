# Lab 3
# Clone your fork of the repository from your Github account (using the SSH URL)
git clone git@github.com:jiujiuZ11/lab.git <enter>
<img width="1440" alt="Screenshot 2023-12-03 at 11 51 18 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/601c5f64-81fa-4f2d-9fe7-7664d7933f9a">

# Run the tests, demonstrating that they fail
Type chmod +x test.sh and <enter>
Type ./test.sh and <enter>
chmod +x test.sh, Return: Changes the permission of test.sh to make it executable. chmod is the command to change file modes or Access Control Lists, +x adds execution permissions, and test.sh is the target file.
./test.sh, Return: Tries to execute test.sh.
<img width="1440" alt="Screenshot 2023-12-03 at 11 51 22 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/4b1d2cc6-d6ad-4eb9-948c-32af4d04b56f">

# Edit the code file ListExamples.java to fix the failing test (as a reminder, the error in the code is just that index1 is used instead of index2 in the final loop in merge)
nano ListExamples.java
index1 += 1; to index2 += 1
Ctrl + O
Return
Ctrl + X: Exits nano.\

<img width="1440" alt="Screenshot 2023-12-03 at 11 56 40 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/5321d01a-2d50-4cc3-b7c1-888bf5913858">

