# Step 1: بناء المشروع باستخدام Node.js
FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

# Step 2: خدمة المشروع باستخدام Nginx
FROM nginx:alpine

# نسخ ملفات البناء من المرحلة السابقة
COPY --from=build /app/build /usr/share/nginx/html

# تعيين متغير البيئة لـ API URL
ENV REACT_APP_API_URL=http://backend:5000

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

