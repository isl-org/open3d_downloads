# Open3D-Downloads

Hosting Open3D test data for development use.

## (TL;DR) How to add a data file

- Small files (e.g. several MB)
    - Step 1: Push the file to the `open3d_downloads` repo.
    - Step 2: Get the **direct** download URL to the file. The URL typically
      looks like `https://github.com/intel-isl/open3d_downloads/raw/master/path/to/file`.
      You may get the URL by going to the file in the GitHub website, right
      click on the "Download" button and select "Copy link address".
    - Step 3: Back to the `Open3D` repo, edit
      `Open3D/examples/test_data/download_file_list.py` to specify the
      **direct** download URL and download path.
    - Step 4: Done! When you re-build the `Open3D` project, the new file will
      be downloaded to `Open3D/examples/test_data/open3d_downloads`. Now you
      can use this file in your source code including unit tests.
- Large files (max 2GB)
    - Step 1: Create a new release or re-use an existing release in the
      `open3d_downloads` repo.
    - Step 2: Upload your file as a release artifact. For files larger than 2GB,
      you may split the files into parts with tools like `zip` or `tar`. After
      uploading, you will able to get the **direct** download URL.
    - Step 3: These files will not be downloaded automatically. You need to
      add your own mechanisms to download and consume the files.

## When is the download triggered

Files listed in `Open3D/examples/test_data/download_file_list.py` will be
downloaded automatically in the following scenarios.

- When running CMake config steps
    - During the first CMake config run, the downloader will overwrite existing
      files in `Open3D/examples/test_data/open3d_downloads`. It will not remove
      extra files.
    - In subsequent CMake config re-run, the downloader will download new files
      and will not overwrite existing files (even if the file has been updated
      in the remote URL). To start fresh, you may delete the
      `Open3D/examples/test_data/open3d_downloads` directory and CMake will
      download everything again.
- When running Python unit tests
    - The downloader will download new files and will not overwrite existing
      files.
- When running Python examples/tutorials
    - The downloader will download new files and will not overwrite existing
      files.

## Permission control

Community developers can create pull requests to add new files to the
`open3d_downloads` repo. Internal developers can directly push to the
`open3d_downloads` repo's `master` branch and create/modify releases.
