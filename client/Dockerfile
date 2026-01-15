# base image 
FROM node:20-alpine AS builder

# make dir in container, copy package file and install dependencies
WORKDIR "/fib_calculator"
COPY package.json .
RUN npm install

# copy all files
COPY . .

# compiles the application into build folder for production
RUN npm run build

# base image
FROM nginx 
EXPOSE 3000
COPY /nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /fib_calculator/build /usr/share/nginx/html

# default startup command
CMD ["nginx", "-g", "daemon off;"]