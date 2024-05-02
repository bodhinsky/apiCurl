System Prompt:
----------------
You are an expert software engineer capable of creating patch strings. Create a patch string based on the issue description. Please respond with your analysis directly in JSON format The JSON schema should include: {'patch_string': string (diff --git a/...)}.

User Prompt:
--------------
Please create a detailed implementation proposal for the described task and the following issue based on the provided code base.
Code Base: src/
    apicurl/
        authCurl.py
        __main__.py
    sw_dev_crew/
        crew.py
        runit.py
        config/
            agents.yaml
            tasks.yaml
    diff_patch_search.egg-info/
        PKG-INFO
        SOURCES.txt
        entry_points.txt
        top_level.txt
        dependency_links.txt
    diff_patch_search/
        describe_repo.py
        repo-description.txt
        generate_patch.py
        sandbox.py
        call_openai.py
        __main__.py
        __pycache__/
            call_openai.cpython-311.pyc
            describe_repo.cpython-311.pyc
            generate_patch.cpython-311.pyc
            __main__.cpython-311.pyc
tests/
    main_test.py
        1: from apicurl import authenticate, getdata
        2: 
        3: def test_authenticate_against_api(url: Str):
        4:     assert authenticate(url) == True
        5: 
        6: def test_data_curl(url: Str):
        7:     assert getdata(url)

Issue: I want to implement an app which authenticates against the discogs API and then downloads the users collection and save it to a file
Affected files: {
  "files": [
    {"file": "src/apicurl/authCurl.py"},
    {"file": "src/apicurl/__main__.py"},
    {"file": "src/diff_patch_search/__main__.py"},
    {"file": "src/diff_patch_search/call_openai.py"},
    {"file": "tests/main_test.py"}
  ]
}
Lines to be changed: {
  "implementation_proposal": [
    {
      "file": "src/apicurl/authCurl.py",
      "lines_to_be_changed_in_original_and_changed_file": [
        "@@ -1,2 +1,10 @@"
      ]
    },
    {
      "file": "src/apicurl/__main__.py",
      "lines_to_be_changed_in_original_and_changed_file": [
        "@@ -1,2 +1,10 @@"
      ]
    },
    {
      "file": "src/diff_patch_search/__main__.py",
      "lines_to_be_changed_in_original_and_changed_file": [
        "@@ -1,2 +1,10 @@"
      ]
    },
    {
      "file": "src/diff_patch_search/call_openai.py",
      "lines_to_be_changed_in_original_and_changed_file": [
        "@@ -1,2 +1,10 @@"
      ]
    },
    {
      "file": "tests/main_test.py",
      "lines_to_be_changed_in_original_and_changed_file": [
        "@@ -1,2 +1,10 @@"
      ]
    }
  ]
}
Code snippets for changes: {
  "implementation_proposal": [
    {
      "file": "src/apicurl/authCurl.py",
      "code_snippet": "import requests\n\ndef authenticate(api_key: str):\n    headers = {'Authorization': f'Token {api_key}'}\n    response = requests.get('https://api.discogs.com/users/me', headers=headers)\n    if response.status_code == 200:\n        return True\n    return False"
    },
    {
      "file": "src/apicurl/__main__.py",
      "code_snippet": "from authCurl import authenticate\nimport sys\n\nif __name__ == '__main__':\n    api_key = sys.argv[1]\n    if authenticate(api_key):\n        print('Authentication successful')\n    else:\n        print('Authentication failed')"
    },
    {
      "file": "src/diff_patch_search/__main__.py",
      "code_snippet": "import sys\nfrom call_openai import download_user_collection\n\nif __name__ == '__main__':\n    api_key = sys.argv[1]\n    download_user_collection(api_key)"
    },
    {
      "file": "src/diff_patch_search/call_openai.py",
      "code_snippet": "import requests\n\ndef download_user_collection(api_key: str):\n    headers = {'Authorization': f'Token {api_key}'}\n    response = requests.get('https://api.discogs.com/users/me/collection/folders/0/releases', headers=headers)\n    if response.status_code == 200:\n        with open('user_collection.json', 'w') as file:\n            file.write(response.text)\n        print('Collection downloaded successfully')\n    else:\n        print('Failed to download collection')"
    },
    {
      "file": "tests/main_test.py",
      "code_snippet": "from apicurl.authCurl import authenticate\nfrom diff_patch_search.call_openai import download_user_collection\nimport unittest\n\nclass TestDiscogsAPI(unittest.TestCase):\n\n    def test_authenticate(self):\n        self.assertTrue(authenticate('valid_api_key'))\n\n    def test_download_collection(self):\n        self.assertIsNone(download_user_collection('valid_api_key'))\n\nif __name__ == '__main__':\n    unittest.main()"
    }
  ]
}