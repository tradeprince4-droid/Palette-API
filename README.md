# Palette-API# pip install flask
import colorsys, random
from flask import Flask, jsonify

app = Flask(__name__)

def make(n=5):
    base = random.random()
    out = []
    for i in range(n):
        r, g, b = colorsys.hls_to_rgb((base + i * 0.12) % 1, random.uniform(0.35, 0.7), random.uniform(0.5, 0.8))
        out.append("#%02X%02X%02X" % (int(r * 255), int(g * 255), int(b * 255)))
    return out

@app.get("/palette")
def palette():
    return jsonify(colors=make())

if __name__ == "__main__":
    app.run(port=5000)
