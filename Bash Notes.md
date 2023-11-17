how to create a shortcut executable for any .sh extension: 
	1. go the file locatoin of the executable. copy the file path. 
		1. you can copy the file path in the gui by clicking the three bars and 'copy path location'
	  2. then you go to the .bashrc file with vim
	  3. set up an alias with a comment for description and then have the command cd into the file location (paste location) and then launch the executable. exit the terminal to make it current
	 `alias clion='cd /home/general-iroh/CLion/CLion-2023.2.2/clion-2023.2.2/bin && ./clion.sh'` and then bam you can use that line anywhere. 

How to pipe the contents of a cat to something else:
1. say you have a .sql file 
2. and a database called songs.db
3. run `cat 7.sql | sqlite3 songs.db` 
4. see the fun stuff