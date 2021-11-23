# HTB_Passage
Hello everyone, here we will consider the solution of the Passage machine, which can be found on the special platform Hack The Box.
Well, below is a description of the machine itself and its specific parameters, including the ip-address.

![Screenshot_1](https://user-images.githubusercontent.com/57565730/142983961-82bb86eb-f81b-45c2-ab6a-463418474478.png)

# Machine solution (GET USER)
Progress:
  1. First you need to take a user. More precisely, log into the servers under the login of an existing user, thereby gaining access to some services.
  2. First, we connect openvpn in my case it is

```console
      $ sudo openvpn <your creds>.ovpn
```
      
  3. We have an existing ip address 10.10.10.206, go to it and see a regular news site
  
 ![unnamed](https://user-images.githubusercontent.com/57565730/142984943-4d013b31-b7c6-4130-86bd-a78ecbcf049f.png)
  
  4. I make a header (the header includes viewing directories through dirsearch and viewing open ports using nmap), the search results are small, but at least something:
      - ssh port 22 is open
      - there is port 80 http where the site is located
      - dirsearch gave nothing
  5. I start looking at what is interesting on the site, and I see that there is a news service with a flat file system CuteNews, well, then on a whim I decide to drive CuteNews into the directory of the site, voila, we have an entrance and registration for this service
 
![unnamed1](https://user-images.githubusercontent.com/57565730/142985662-70a14b82-dcbc-44ff-a4c9-3a317d6fcc3d.png)

  6. At first I spent a lot of time on brute-force login and password, but in the end I decided to just register, then I go into personal settings and see that there is a file upload, which is very often a big vulnerability ... well, here we have, as it were, php, which means ideas here you can throw php code ...
  7. In general, I wrote a one-line php code that sets a request for a shell command:
 
![unnamed2](https://user-images.githubusercontent.com/57565730/142985823-3e8afa9c-1b8c-4986-aace-6426e073e740.png)

  8. Next, I upload this php code to uploads, and look for myself, after which I write a command for the shell
   
 ![unnamed3](https://user-images.githubusercontent.com/57565730/142985956-6e82a667-10a0-4bfb-9d03-f1ffa36c7589.png)
 ![unnamed4](https://user-images.githubusercontent.com/57565730/142986053-d98c393a-1404-4ac7-bcb8-0e851b1d84a8.png)

  9. Ok, I was able to see with the bash command who I am and ls files, so logically I can do a reverse shell, do ... We get access to the server in 2 steps:

![unnamed5](https://user-images.githubusercontent.com/57565730/142986201-1ca575ea-d671-405f-8f3c-7741836dde6a.png)

Step 1
                                                
![unnamed6](https://user-images.githubusercontent.com/57565730/142986335-3ae5a2d5-2e8c-48e5-8fcd-a7f50e82bcf4.png)           

Step 2

As a result, we throw the reverse shell, now we are on the server side, congratulations, but this is just the beginning.

  10. And so we are on the server, but as web-data, we are still nobody, but this will change soon, then the routine work begins, browsing directories and looking for something interesting ....

![unnamed7](https://user-images.githubusercontent.com/57565730/142986567-e5481c77-6ca9-481d-b951-204fa9cf6adc.png)

After 2.5 hours, I came across the www directory:

![unnamed8](https://user-images.githubusercontent.com/57565730/142986823-acec6f56-1736-48c9-816c-fed6a4a7e8b8.png)

After going through some files, I came to the b0.php file

![unnamed9](https://user-images.githubusercontent.com/57565730/142986918-8f90a261-2bc8-418e-83bf-cb24643a2289.png)

Looking at the structure of the cipher, I immediately realized that it was base64, as a result of which I used the site decoder ...

![unnamed10](https://user-images.githubusercontent.com/57565730/142987026-62750099-9794-4774-b3cf-e9a61808f5f1.png)

There is a hash password inside, there is even this written there, I also google the hash decode site and this result comes out ...

![unnamed11](https://user-images.githubusercontent.com/57565730/142987236-98153554-871c-4290-a932-861140327ca0.png)

>Login: paul

>Password: atlanta1

  11. It remains only to log in as a user

![unnamed12](https://user-images.githubusercontent.com/57565730/142987425-f7c08e8d-3979-4350-862d-00a7cdde2e6c.png)

We are in the system!


