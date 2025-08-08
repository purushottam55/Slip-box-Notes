Tmux

To create new screen 


tmux new -s datacopy

without killing out

$ Ctl+b d = > 

List screens
# tmux ls

Get into the screen
tmux a -t datacopy

Terminate the process 
In the screen ctl+c


Grub passwd :

grub2-mkpasswd-pbkdf2

grub2-mkconfig -o /boot/grub2/grub.cfg



Change password user :


for server in server1 server2 server3; do
  ssh root@"$server" "echo -e 'NewPass123\nNewPass123' | passwd testuser"
done


Notepad++ trick for servers

Paste the servers from the sheet  in the notepad++  >> select all data >> Go to find replace >>  replace with \n\p to " "


Zipping 
tar -cvzf /tmp/rhd.jejs abcName.zip

redhat-suppoort-tool addattachment -c 636363673 /tmp/drrhds1 ,



tail -f var/log/secure


Register server 


nc -vz ip port

=======


$ nmap -p- destinationIP

Also see :
