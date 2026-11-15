# Lychee Juicebox

This repository groups the two Lychee Juicebox codebases as Git submodules:

| Folder | Repository | Contents |
| --- | --- | --- |
| `web-and-map-api/` | [TeamLychee_NasaSpaceApps](https://github.com/Mretmna/team-lychee-nasaspaceapps-27) | Next.js app in `frontend/` and map API in `backend/` |
| `sound-api/` | [TeamLychee_NasaSpaceApps_Backend](https://github.com/Mretmna/team-lychee-nasaspaceapps-backend-27) | FastAPI sound service in `backend/` |

Clone both codebases with:

```sh
git clone --recurse-submodules https://github.com/Mretmna/lychee-juicebox.git
```

If you already cloned this repository, run `git submodule update --init --recursive` from its root.

The submodules remain independent repositories. Commit and push code changes inside the relevant submodule, then commit its updated reference here when you want the parent to point at that version. Existing deployments continue using their current repositories; this parent repository does not configure or change them.
