# code
PROBLEM 1
class Delta:
    def __init__(self, position, old_text, new_text):
        self.position = position
        self.old_text = old_text
        self.new_text = new_text

class FileVersioning:
    def __init__(self, base_version, deltas):
        self.base_version = base_version
        self.deltas = deltas

    def get_file_version(self, version):
        if version < 0 or version > len(self.deltas):
            raise ValueError("Invalid version")
        
        file = self.base_version
        for i in range(version):
            delta = self.deltas[i]
            start_index = delta.position
            end_index = start_index + len(delta.old_text)
            file = file[:start_index] + delta.new_text + file[end_index:]
        
        return file


base_version = "Hello, world!"
deltas = [
    Delta(7, "world", "Python"),
    Delta(0, "Hello", "Hi")
]

file_versioning = FileVersioning(base_version, deltas)
try:
    print(file_versioning.get_file_version(1))  # Output: "Hello, Python!"
    print(file_versioning.get_file_version(2))  # Output: "Hi, Python!"
except ValueError as e:
    print(e)

