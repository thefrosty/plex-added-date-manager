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

`PLEX_MOVIE_SECTION_ID` and `PLEX_TV_SECTION_ID` set the library selected when the app opens. They default to `1` and `2`. Each tab also has a section menu for the other movie and TV libraries on the server.

Stop the app with Ctrl+C, then:

```bash
docker compose down
```

## Usage

Movies and TV Series each load one page at a time, with page sizes of 50, 100, or 200. Sort by added date, title, or year, and filter by year. "Title contains" narrows the items on the current page.

Select items across pages and apply one added date to the whole selection. "Lock added date" tells Plex to keep that field. Turn images off when a page feels heavy.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.
