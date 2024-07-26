# **Set Username**

You'll do this from your terminal.

To set your Git username, type this in your terminal:
    *git config --global user.name "username"*

To confirm that you have set your Git username correctly, type this:
    *git config --global user.name*
    
 You should have "username" as the output.
    
# **Set Email**    

To set your Git email, type this in your terminal:
    *git config --global user.email "youremail@gmail.com"*
    
To confirm that you have set your Git email correctly, type this:
    *git config --global user.email*
    
You should have "youremail@gmail.com" as the output.

You will be asked to authenticate your GitHub account, so just sign in with the same email to confirm.

# Create a Repository on GitHub

Click the *+* sign at the top right corner to create a new repository. Repositories are like your code folders online.

You will be prompted to create a new repository page. Name the repository and add a description.

Create the repository.

# Push your local code to GitHub

You can use the code editor built-in terminal to use Git to push your code to GitHub. Click `ctrl + shift + '` to open the terminal in VSCode.

Input the commands below one after the other in your terminal. Press the Enter key to proceed after every input.

    echo "# sample-code" >> README.md
    git init
    git add .
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/username/sample-code.git
    git push -u origin main

# Move Existing Folders

To move existing folders within your GitHub repository using the web interface, you can manually move the files from one folder to another and then delete the empty folders. Here's a step-by-step guide:
   
1. Navigate to Your Repository:
    Go to your GitHub account and navigate to the repository you want to restructure.
        
2. Move Files to New Folders:
For each file in the folder you want to move, navigate to that file.
Click on the file to open it.
        
3. Click on the pencil icon (Edit this file) in the top right corner.
    
4. In the "Name your file" field, change the file path to the new folder location. For example, if you want to move `existingfolder/file.md` to `newfolder/existingfolder/file.md`, change the path accordingly.
    
5. Scroll down and click on "Commit changes". Repeat this for each file in the folder.
   
6. Delete Empty Folders: Once all files have been moved, navigate to the old, now empty folder. Delete the folder by clicking the "Delete directory" button, if available. If this button is not available, the folder will be removed automatically once it is empty.
