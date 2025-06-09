# Docker-compose
Group B project task

✅WEEK 4 MENTORSHIP PROJECT BY GROUP B TEAM

✅GROUP B TEAM: Fagoroye Sanumi O.
                 & Lawal Jonathan

📌**TOPIC**: Containerize a Web App using Docker Compose

🔗 **How Containers Communicate and Persist Data**

This project uses Docker Compose to orchestrate a multi-container setup comprising a Flask web application and a PostgreSQL database. Understanding how these containers communicate and how data persistence is achieved is critical for reliable and maintainable deployment.

1. **Container Communication**

Both the Flask app and PostgreSQL database are defined as separate services in docker-compose.yml, connected via a custom Docker network named cool_network.

Docker Compose automatically creates this network and allows containers to discover and communicate with each other using their service names as hostnames.

Inside the Flask application (app.py), the database connection uses the service name db as the hostname, enabling seamless networking without exposing database ports externally.

The depends_on directive in docker-compose.yml with the condition: service_healthy setting ensures the Flask app container waits until the PostgreSQL service passes its health check before starting, preventing connection errors at startup.

2. **Data Persistence**

Containers are ephemeral by design; if the PostgreSQL container stops or is removed, any data stored inside the container filesystem is lost.

To avoid this, the database service mounts a named Docker volume postgres_data_new to the Postgres data directory /var/lib/postgresql/data

This volume exists outside the container’s lifecycle, persisting data on the host machine.

When the container restarts or is recreated, PostgreSQL reads and writes data directly to this volume, preserving the database state.

3. **Environment Variables and Security**
Sensitive information such as database username, password, and database name are stored in a .env file referenced in the Compose file under env_file: .env.

This approach separates configuration from code, enabling easier management and improved security.

📘**Summary**

Networking- Both containers connect via cool_network. The Flask app uses db as the hostname to reach PostgreSQL.

Startup Order- depends_on + healthcheck ensure the database is ready before the Flask app starts.

Data Persistence- Postgres data stored in a Docker named volume postgres_data_new outside the container’s lifecycle.

Configuration- Environment variables stored in .env file for security and flexibility.

✅**proof of the local app working using docker-compose up**

![Docker](<Images/Screenshot 2025-06-09 124950.png>)

![Page](<Images/Screenshot 2025-06-09 123727.png>)

![Page2](<Images/Screenshot 2025-06-09 123955.png>)

![Page3](<Images/Screenshot 2025-06-09 123658.png>)
