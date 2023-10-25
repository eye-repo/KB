# Printing

    import json
    print(json.dumps(info, indent=4))

# Open and Save to file

Simple:

    with open('Failed.py', 'w') as file:
        file.write('whatever')

Save to JSON

    import json
    jdata = {
        "1": ["a", "b"],
        "2": "c" 
    }
    filepath = "/path/file.json"
    with open(filepath, 'w', encoding='utf-8') as f:
        json.dump(jdata, f, ensure_ascii=False, indent=4)

Open JSON file

    with open(filepath, 'r', encoding='utf-8') as f:
        data = json.load(f)
