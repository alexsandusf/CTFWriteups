# pcap-busterz-1
## I have intercepted a pcap file on the dark web between unknown agents. Help me decrypt it and find out what they're upto!!


### Step 1:
Follow TCP stream with wireshark on the PCAP file
We get a list of X Y coordinantes and colors black or white

Lets plot each point using python:


```python
import matplotlib.pyplot as plt

def parse_data(file_path):
    data = []
    with open(file_path, 'r') as file:
        for line in file:
            line = line.strip()
            if line:
                parts = line.split(', ')
                entry = {}
                for part in parts:
                    key, value = part.split('=')
                    entry[key] = value
                data.append(entry)
    return data

file_path = "data.txt"  # Replace this with the path to your text file
formatted_data = parse_data(file_path)

# Extract coordinates and colors from formatted data
coordinates = [(int(entry['x']), int(entry['y'])) for entry in formatted_data]
colors = [entry['color'] for entry in formatted_data]

# Unpack coordinates into separate lists
x_values, y_values = zip(*coordinates)

# Create scatter plot
plt.figure(figsize=(8, 6))
plt.scatter(x_values, y_values, c=colors)

# Add labels and title
plt.xlabel('X-coordinate')
plt.ylabel('Y-coordinate')
plt.title('Scatter Plot of Coordinates with Colors')

# Show plot
plt.grid(True)
plt.show()
```


The resulting image: 

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/505c48db-6938-482e-a75b-41aeceb49971)



# Step 2:
Scan the qr code and we get the flag

pearl{QR_rev0lution1ses_mod3rn_data_handl1ng}




