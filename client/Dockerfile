from node:14-alpine as builder
# Set the working directory
WORKDIR '/app'

# Copy package.json and package-lock.json files
COPY ./package.json ./

# Install npm dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

RUN npm run build 
#after executing this build command this will create a new build folder under app directory that contain all build assets.
from nginx
expose 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# we also need to copy all production build assets from the builder phase.
COPY --from=builder /app/build/ /usr/share/nginx/html