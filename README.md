# day-12
def read_requirements(file):
    data = {"Project": "", "Timeline": "", "Priority": "", "Features": []}
    try:
        with open(file, "r") as f:
            for line in f:
                line = line.strip()
                if line.startswith("Project:"):
                    data["Project"] = line.split(":", 1)[1].strip()
                elif line.startswith("Timeline:"):
                    data["Timeline"] = line.split(":", 1)[1].strip()
                elif line.startswith("Priority:"):
                    data["Priority"] = line.split(":", 1)[1].strip()
                elif line.startswith("-"):
                    data["Features"].append(line.lstrip("- ").strip())
    except FileNotFoundError:
        print(f"Error: File '{file}' not found.")
        return None
    return data

def write_summary(data):
    if not data:
        return
    summary = f"""Project Summary Report
-------------------------
Project: {data['Project']}
Timeline: {data['Timeline']}
Priority: {data['Priority']}
Features to Implement:"""
    for f in data["Features"]:
        summary += f"\n - {f}"
    print(summary)
    with open("project_summary.txt", "w") as f:
        f.write(summary)

data = read_requirements("client_requirements.txt")
write_summary(data)
