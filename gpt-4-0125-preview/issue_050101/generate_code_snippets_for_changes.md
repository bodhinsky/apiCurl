{
"file": "src/apiCurl/fetchUserCollection.py",
"code_snippet": "1: from importCredentials import getUserCredentials\n2: import requests\n3: \n4: def get_user_collection(page=1):\n5:     \"\"\"Fetches a user's collection from Discogs for a specified page.\n6: \n7:     Args:\n8:         page (int, optional): The page number to fetch. Defaults to 1.\n9: \n10:     Returns:\n11:         tuple: A tuple containing the list of releases and either the URL to the next page or False if there is no next page.\n12:     \"\"\"\n13:     user_name, user_token = getUserCredentials(service='Discogs')\n14: \n15:     headers = {\n16:         'Authorization': f'Discogs token={user_token}',\n17:         'User-Agent': 'DiscogsCollectionExporter/1.0'\n18:     }\n19:     url = f'https://api.discogs.com/users/{user_name}/collection/folders/0/releases?page={page}'\n20: \n21:     try:\n22:         response = requests.get(url, headers=headers)\n23:         response.raise_for_status()  # Raise an exception for bad status codes\n24:         collection_data = response.json()\n25:         max_pages = collection_data['pagination']['pages']\n26:         if page < max_pages:\n27:             return collection_data['releases'], collection_data['pagination']['urls']['next']\n28:         else:\n29:             return collection_data['releases'], False\n30:     except requests.exceptions.RequestException as e:\n31:         print(f\"Error fetching collection: {e}\")\n32:         return [], False\n33: \n34: def fetch_all_collection_pages():\n35:     \"\"\"Fetches all pages of a user's collection from Discogs.\n36: \n37:     Returns:\n38:         list: A list of all releases in the user's collection.\n39:     \"\"\"\n40:     all_releases = []\n41:     next_page = True\n42:     page_number = 1\n43: \n44:     while next_page:\n45:         releases, next_page_url = get_user_collection(page_number)\n46:         next_page = next_page_url\n47:         all_releases.extend(releases)\n48:         page_number += 1\n49: \n50:     return all_releases\n"
}