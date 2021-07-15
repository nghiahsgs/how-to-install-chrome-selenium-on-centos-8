# how-to-install-chrome-selenium-on-centos-8
how to install chrome selenium on centos 8

## Install all essential packages
```
sudo yum update
optional
sudo yum install -y unzip openjdk-8-jre-headless xvfb libxi6 libgconf-2-4
```

##  Make sure you have below info in the file(remove hash).
```
vi /etc/yum.repos.d/google-chrome.repo
```

```
[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/x86_64
enabled=1
gpgcheck=1
gpgkey=https://dl-ssl.google.com/linux/linux_signing_key.pub
```

```
yum install -y google-chrome-stable
```

```
google-chrome --version
```

## Install ChromeDriver.
chromedriver version depend on chrome version
You need to get link download newest chrome selenium on https://chromedriver.chromium.org/downloads. For examples: current chrome version is v79
```
wget -N https://chromedriver.storage.googleapis.com/91.0.4472.101/chromedriver_linux64.zip -P ~/
unzip ~/chromedriver_linux64.zip -d ~/
rm ~/chromedriver_linux64.zip
sudo mv -f ~/chromedriver /usr/local/bin/chromedriver
sudo chown root:root /usr/local/bin/chromedriver
sudo chmod 0755 /usr/local/bin/chromedriver
```

## Python
```
pip install selenium
```

```
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
CHROMEDRIVER_PATH = '/usr/local/bin/chromedriver'
WINDOW_SIZE = "1920,1080"
chrome_options = Options()
chrome_options.add_argument("--headless")
chrome_options.add_argument("--window-size=%s" % WINDOW_SIZE)
chrome_options.add_argument('--no-sandbox')
driver = webdriver.Chrome(executable_path=CHROMEDRIVER_PATH,
                          chrome_options=chrome_options
                         )
driver.get("https://www.google.com")
print(driver.title)
driver.close()
```
