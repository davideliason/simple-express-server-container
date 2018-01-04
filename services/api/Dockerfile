# Use an official Node runtime as parent image
FROM node:9.3.0

# set working directory to /app
WORKDIR /app

# copy current directory contents into /app
ADD . /app

# install express dependency
RUN npm install

# make port 8080 available to the outside world outside this container
EXPOSE 8080

# run index.js when the container launches
CMD ["node","index.js"]