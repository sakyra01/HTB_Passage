# HTB_Passage
Hello everyone, here we will consider the solution of the Passage machine, which can be found on the special platform Hack The Box.
Well, below is a description of the machine itself and its specific parameters, including the ip-address.

![Screenshot_1](https://user-images.githubusercontent.com/57565730/142983961-82bb86eb-f81b-45c2-ab6a-463418474478.png)

# Machine solution (GET USER)
Progress:
  1. First you need to take a user. More precisely, log into the servers under the login of an existing user, thereby gaining access to some services.
  2. First, we connect openvpn in my case it is

```console
      - $ sudo openvpn <your creds>.ovpn
```
      
  3. We have an existing ip address 10.10.10.206, go to it and see a regular news site
  
  ![unnamed](https://user-images.githubusercontent.com/57565730/142984943-4d013b31-b7c6-4130-86bd-a78ecbcf049f.png)
