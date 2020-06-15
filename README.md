# magento2docker-compose
## Prerequisites:

- Install Docker
- Install Composer
- Download Magento 2
## Setup Steps:

- Create docker-compose.yml file
- Spin up Docker containers
- Install Magento with optional sample data

Log in or create an account on Magento marketplace. Once logged in, navigate to Access Keys and keep that window open as you will need the keys in step #3.
Determine a location on your local machine where you would like the website files to live.
Open up a command line terminal. Before copying and pasting the code below, replace the placeholder path with the absolute path of where you plan to download/install Magento.
`cd /path/to/where/you/will/download/magento && \
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .`
The latest version of Magento 2 is now downloaded to your machine. From this point forward, we will refer to the directory where you installed Magento as /path/to/magento.
Increase the PHP memory limit from the default value of 756M to 2048M.
`find . -name '.htaccess' -exec sed -i '' s/756M/2048M/g {} + && \
find . -name '.htaccess' -exec sed -i '' s/768M/2048M/g {} + && \
find . -name '.user.ini' -exec sed -i '' s/756M/2048M/g {} + && \
find . -name '.user.ini' -exec sed -i '' s/768M/2048M/g {} +`
Choose a domain name you would like to use to access the site and add it to your hosts file.
`sudo -- sh -c "echo '127.0.0.1 local.domain.com' >> /etc/hosts"`

At this point in time, your terminal should still be open to /path/to/docker.
Fire up your virtual machine! The first time you spin up, Docker needs to download the images, this may take a few minutes. Future spin-ups will only take a few seconds, usually less than 10.
`docker-compose up -d --build`
Let’s make sure that it’s up and running as planned. In a web browser, go to `127.0.0.1:8080` and make sure that you can see phpMyAdmin. If you can, it was a success.

- Access your Docker web container’s command line.
`docker exec -it web bash`
- Navigate to the web document root.
`cd /app`
- Optional but recommended: deploy sample data.
`php bin/magento sampledata:deploy`
