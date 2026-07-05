FROM node:20-slim
WORKDIR /app

# Install python, pip, and build tools
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python-is-python3 \
    build-essential \
    cmake \
    libopenblas-dev \
    liblapack-dev \
    libx11-dev \
    && rm -rf /var/lib/apt/lists/*

# Copy package files
COPY package*.json ./
RUN npm install

# Copy source code
COPY . .

# Install Python requirements (limit cmake parallel jobs to 1 to prevent OOM)
ENV CMAKE_BUILD_PARALLEL_LEVEL=1
RUN pip install --no-cache-dir -r requirements.txt --break-system-packages

# Build the TypeScript project
RUN npm run build

EXPOSE 3000
CMD ["npm", "start"]
