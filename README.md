# OS

FTP Server

Step1: Update package index using following command
            sudo apt update
Step2: Install ftp server by the command
            sudo apt install vsftpd
Step3: Checking the status of the ftp server
             sudo service vsftpd status
           {The server should be running}
Step4: Configure ftp server
           sudo nano /etc/vsftpd.conf
           {In the file}
           Make local_enable=YES
           write_enable=YES
           chroot_local_user=YES
           user_sub_token=$USER
           local_root=/home/$USER/ftp
           pasv_min_port=10000
           pasv_max_port=10100 
           userlist_enable=YES
           userlist_file=/etc/vsftpd.userlist
           userlist_deny=NO
           Add all of the lines
Press ctrl+X → Y → Enter

Step5: Configure firewall and open these ports
sudo ufw allow from any to any port 20,21,10000:10100 proto tcp

Step6: add user
sudo adduser phil 


Step7: create ftp folder for the user in the home directory
Sudo mkdir /home/phil/ftp

Step8: run the command to configure permissions
sudo chown nobody:nogroup /home/phil/ftp

Step9: permission for the home directory
sudo chmod a-w /home/phil/ftp

Step10: make upload folder for the user
Sudo mkdir /home/phil/ftp/upload

Step11: upload ownership for the user
sudo chown phil:phil /home/phil/ftp/upload

Step12: make demo file into the upload folder
echo “My ftp server” | sudo tee /home/phil/ftp/upload/demo.txt

Step13: check the ftp permission of the file by the command
sudo ls -la /home/phil/ftp


Step14: login and access the ftp server
Echo “phil” | sudo tee -a /etc/vsftpd.userlist

Step15: restarting ftp server
Sudo systemctl restart vsftpd

Step16: checking IP address of the machine to check whether user has the access to ftp server
Ifconfig —> then copy first IP address

Step17: install filezilla and input IP address(host), password and username and do quickconnect 
You will get an upload folder and inside that demo.txt file

sudo service vsftpd stop
