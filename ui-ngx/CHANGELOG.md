# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-xx-xx

Based on ThingsBoard v4.3.0.

### Added

- Platform version number and contact information in the footer of the user menu.

### Changed

- UI rebranded (title, logo, and colors).
- Hide selected widgets in Home page for all users.

### Removed

- Display of the ThingsBoard version from dashboards.
- Certain navigation options from the application menu.

---

### Technical notes

- **Widget filtering**: Implemented a filter function in `dashboard-page.models.ts` that excludes widgets by title.
- **Navigation cleanup**: Menu items were disabled by commenting out their configuration entries in `menu.models.ts`.
- **Version & contact info**: The platform version number is defined in `package.json` and rendered alongside contact details in the user menu footer in `user-menu.component.ts`.
