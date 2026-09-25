# Plex Added Date Manager

Streamlit (Python) app that interacts with the Plex API to fetch and manage Added Date values.

<img alt="screen" src="https://github.com/user-attachments/assets/4d897988-9c44-4737-b4cf-eb4a53379d92" />

## Setup Instructions

Run the app in a container so its Python environment stays off the host.

1. **Create your env file** from the example and fill in your Plex server:
   ```bash
   cp .env.example .env
   ```
2. **Start the app:**
   ```bash
   docker compose up --build
   ```
3. **Open** `http://localhost:8501`.

`PLEX_BASE_URL` is requested from inside the container, so it has to be an address the container can reach. For Plex on
this machine, use `http://host.docker.internal:32400`. For Plex on another machine, use that machine's address, for
example `http://192.168.1.20:32400`.

When Plex requires secure connections, its certificate is issued for a `plex.direct` name. Use that name as
`PLEX_BASE_URL`. A raw IP address fails certificate verification.

`PLEX_MOVIE_SECTION_ID` and `PLEX_TV_SECTION_ID` choose which libraries to edit. They default to `1` and `2`.

Stop the app with Ctrl+C, then:

```bash
docker compose down
```

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
