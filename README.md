# Stash Task

Stash Task is a full stack web application powered by Go (Backend) and Next.js (Frontend). It includes a PostgreSQL database and utilizes Docker Compose for a seamless local development and deployment experience.

## Tech Stack
- **Frontend:** Next.js, React
- **Backend:** Go
- **Database:** PostgreSQL
- **Infrastructure:** Docker & Docker Compose

## Prerequisites
- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Getting Started

To get a local copy up and running, follow these simple steps:

1. **Clone the repository:** 
   ```bash
   git clone https://github.com/micaelcf/stash-task.git
   cd stash-task
   ```

2. **Configure Environment Variables:** 
   Copy the provided example environment file and update the variables if necessary.
   ```bash
   cp .env.example .env
   ```

3. **Start the Application:** 
   Run the following command to build and start the containers in detached mode:
   ```bash
   docker-compose up -d --build
   ```

4. **Access the Application:** 
   - **Frontend:** [http://localhost:3000](http://localhost:3000)
   - **Backend API:** [http://localhost:8080](http://localhost:8080)
   - **PostgreSQL Database:** `localhost:5432`

## Stopping the Application

To stop the running containers, simply run:
```bash
docker-compose down
```

## Contributing
Contributions are welcome! Please fork the repository and open a pull request.

## License
Distributed under the MIT License.