# Use your local pc proxy for your lab server
This is a tutorial teaching you how to configure network proxy for your lab server. If you are blessed to be a Chinese researcher, you may find this tutorial very helpful. \
First, you need to set your local pc to the status that can be be used as a proxy.
## Allow your pc can be used as proxy
For the purpose of copyright protection, I should clarify that the content of this part origins from the web: https://blog.csdn.net/weixin_44576482/article/details/128667675
\
In short, you first need to make sure that the setting "Allow LAN" of your Clash has been set to "open". \
Second, open the terminal of your pc and use command `ipconfig`. Find the IPv4 address of your pc. \
Then, enter the setting setting interface shown below:\
![image](https://github.com/Blanca-s/Chinevenient-Lab-Server/blob/main/imgs/1.png)\
After clicking the "advanced setting" shown in the above image, you will enter a interface like:\
![image](https://github.com/Blanca-s/Chinevenient-Lab-Server/blob/main/imgs/2.png)\
Clicking in accordance with the image above, you will get another interface like:\
![image](https://github.com/Blanca-s/Chinevenient-Lab-Server/blob/main/imgs/3.png)\
Clicking the content framed in red boxes in order and you will get:\
![image](https://github.com/Blanca-s/Chinevenient-Lab-Server/blob/main/imgs/4.png)\
Choose "TCP" and enter the port number given by the "Proxy config" shown on your Clash. \
Create this new rule and your pc will be allowed to be used as a proxy. 
## Create connection
Then, please forget about the operations given by the web I provided at the beginning and do as I say.\
First, establish SSH connection between your pc and your lab server use the following command:
```
ssh -R 51188:127.0.0.1:51188 -p port-of-your-server username@ipaddress-of-your-server
```
Note that `51188` is the proxy configuration of my Clash. If yours is different, change it to yours. \
And please note that the above command should be executed on your local pc, not your lab server.\
When the above command is successfully executed by your local pc, you will be required to input the password. Just input.\
So now, you have already connected your local pc and lab server together. Next you need to do is adding the following content to the enviornment variables of your lab server:
```
export http_proxy=http://127.0.0.1:51188
export https_proxy=http://127.0.0.1:51188
```
> [!Tip]
> If you are not familiar with how to add environment variables, here are the instrunctions:\
> Use command `vi ~/.bashrc` to enter the related file. \
> Simply press `i` to enter the insert mode.\
> Copy and paste the above content to the last part of this file.\
> Simply press `esc` to quit the insert mode.\
> Press `:` and `wq` to save and quit.\
> Use command: `source ~/.bashrc` to make it happen. 

## Test
Use command: `curl -v https://www.google.com`\
If the content on the website is presented on the terminal, you are all set.