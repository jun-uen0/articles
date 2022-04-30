Written with [Cameron Gibson](https://github.com/cgcamcam) 

### Versions
Homebrew 3.4.7
Nginx 1.21.6
Ngrok 3.0.2

### About Ngrok
- A tool that makes the specific port of local machine public on internet
- Pricing: Free for personal use
- Official website: https://ngrok.com/

### Make your local port public to the internet 

- Create your ngrok account at [signup page](https://dashboard.ngrok.com/signup).
- Confirm your email verification
- Install Ngrok following [download page](https://ngrok.com/download)
   ```shell
   brew install ngrok/ngrok/ngrok
   ```

- Get authentication token and command to run at ]Ngrok console "Getting Started > setup & installation"](https://dashboard.ngrok.com/get-started/setup)
   ```shell
   ngrok config add-authtoken <your authentication token>
   ```
- Run Nginx
   ```shell
   nginx
   ```
      
   Acess to http://localhost:8080/
   

- Run Ngrok
   ```shell
   ngrok http 8080
   ```
- Check "Forwarding URL" given
- Acess to "Forwarding URL"