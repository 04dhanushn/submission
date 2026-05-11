# Part 3: Prompt Preparation

## Selected Pull Request

Selected PR: https://github.com/beetbox/beets/pull/3145

This pull request from the beets repository focuses on adding playlist query support using M3U playlist files.

---

## 3.1.1 Repository Context

The beets repository is an open-source music library management system mainly designed for organizing and maintaining digital music collections. It helps users automatically manage music metadata, rename audio files, organize folders, and maintain structured music libraries. Instead of manually editing every song file, users can automate tagging and music organization tasks through plugins and query features available in the system.

The repository is mainly used by music enthusiasts, developers, and users who maintain large collections of audio files. Since beets supports a plugin-based architecture, users can extend the functionality based on their requirements. The system also supports integration with external music players and playlist tools, making it useful for users who work with different music management applications.

The repository mainly addresses problems related to music organization, metadata management, playlist handling, and media library automation. Without tools like beets, managing large music collections manually can become difficult and time-consuming. The selected pull request focuses on improving playlist-based querying support by allowing users to search songs in the library using M3U playlist files. This feature improves compatibility with external playlist systems and simplifies playlist management inside beets.

---

## 3.1.2 Pull Request Description

The selected pull request introduces a playlist query plugin that allows users to search songs in the beets music library using M3U playlist files. Before this update, users could organize music collections inside beets, but there was no direct support for querying tracks through playlist files. Users had to manually filter tracks or use external tools to manage playlist-based searches.

The PR adds a new `PlaylistQuery` implementation that reads playlist files, extracts track paths, and compares them with songs available in the beets library. The implementation supports both full playlist file paths and playlist names stored inside a configured playlist directory. The update also introduces flexible path handling through configuration options such as `playlist_dir` and `relative_to`. These settings help users configure how playlist paths should be interpreted relative to different directories.

Additional validation was added to ensure that only valid `.m3u` playlist files are processed. The implementation also safely handles empty playlists and missing playlist files to avoid application crashes. Documentation updates and unit tests were included to verify the new functionality. Compared to the previous behavior, users can now directly integrate playlist-based workflows into the beets library system.

---

## 3.1.3 Acceptance Criteria

- The system should correctly read valid `.m3u` playlist files.
- Users should be able to query songs using playlist names.
- Users should also be able to query songs using full playlist file paths.
- Playlist entries should correctly match tracks stored in the beets library.
- The `relative_to` configuration should correctly support library paths, playlist paths, and custom directories.
- Invalid or unsupported playlist files should not crash the application.
- Empty playlists should safely return empty query results.
- Playlist comment lines should be ignored during processing.
- All playlist-related unit tests should pass successfully.

---

## 3.1.4 Edge Cases

- Handling empty playlist files that contain no track entries.
- Handling missing or non-existing playlist files.
- Ignoring unsupported playlist formats that are not `.m3u` files.
- Ignoring comment lines inside playlist files.
- Handling incorrect relative path configurations.
- Preventing failures when playlist paths contain unsupported or invalid characters.
- Handling playlists with duplicate song entries.

---

## 3.1.5 Initial Prompt

You are working on the beets music library management repository.

Implement a playlist query feature that allows users to search library tracks using M3U playlist files. The implementation should support reading playlist files, extracting track paths, and matching them with songs stored inside the beets music library.

Requirements:

- Create a custom playlist query implementation that integrates with the existing beets query system.
- Support `.m3u` playlist files.
- Allow querying playlists using both full playlist file paths and playlist names.
- Add configuration support for:
  - `playlist_dir`
  - `relative_to`
- Support relative path handling for playlist entries.
- Ignore comment lines and unsupported entries inside playlist files.
- Ensure invalid playlist files do not cause application crashes.
- Safely handle empty playlists.
- Normalize playlist paths before comparing them with library items.

Acceptance Criteria:

- Valid playlist files should return matching library tracks.
- Querying by playlist name should work correctly.
- Querying by full playlist path should work correctly.
- Empty playlists should return empty results safely.
- Invalid playlists should not break the application.
- Playlist paths should work correctly with different relative path configurations.
- Existing query functionality in beets should remain unaffected.

Edge Cases:

- Missing playlist files.
- Invalid playlist extensions.
- Comment lines inside playlist files.
- Relative path mismatches.
- Unsupported playlist entries.
- Duplicate tracks inside playlists.

Testing Requirements:

- Add unit tests for playlist name queries.
- Add unit tests for full playlist path queries.
- Add tests for missing playlist handling.
- Verify empty playlists return empty results.
- Ensure all existing tests continue to pass.

Documentation Requirements:

- Update plugin documentation.
- Add usage examples for playlist queries.
- Document configuration options and supported behaviors.
