#tentukan OS
FROM node:18.20.8-slim 

#membuat folder 
WORKDIR /app

#Masukin app ke folder kedalam container 
ADD . /app/

#build aplikasi
RUN npm install 

#jalankan aplikasi
CMD ["npm", "start"]
