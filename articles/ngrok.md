### The goal of the article
- Publish a website
- Website page: Nginx Welcome page!」

### Local Everonment
OS: macOS ver 12.1　(intel chip)
Homebrew 3.4.7
Nginx 1.21.6
Ngrok 3.0.2

### About Ngrok
- A tool that makes specific port of local mahchine pablic on internet
- Pricing: Free for personal use
- Official website: https://ngrok.com/

### Make your local port public to internet 

1. Create your ngrok account at [signup page](https://dashboard.ngrok.com/signup). Then check your email verification
2. Install Ngrok folloing [download page]((https://ngrok.com/download)
```shell
brew install ngrok/ngrok/ngrok
```
3. Get authentication token and command to run at ]Ngrok console "Getting Started > setup & installation"](https://dashboard.ngrok.com/get-started/setup)
```shell
ngrok config add-authtoken <your authentication token>
```
4. Run Nginx
```shell
nginx

# Then access to http://localhost:8080/
# Make sure you see Nginx welcome page at localhost:8080
```
5. Run Ngrok
```shell
ngrok http 8080

# Access to the url given
# Make sure you see Nginx welcome page at the url
```