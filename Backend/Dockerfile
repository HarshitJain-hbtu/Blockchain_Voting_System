FROM node:20-slim
WORKDIR /app

# Install python, pip, and pre-built dlib (to avoid cmake OOM on Render)
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python-is-python3 \
    python3-dlib \
    python3-numpy \
    libopenblas-dev \
    liblapack-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy package files
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Install Python requirements (will use system dlib)
RUN pip install -r requirements.txt --break-system-packages

# Build the TypeScript project
RUN npm run build

EXPOSE 3000
CMD ["npm", "start"]
