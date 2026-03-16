#!/bin/bash

# Generate gerber files and drill files for OSH Park fabrication
# Requires: kicad-cli (installed with KiCad)

set -euo pipefail

SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"
PROJECT_DIR="$(dirname "$SCRIPT_DIR")"
PCB_FILE="$PROJECT_DIR/tdcs.kicad_pcb"
OUTPUT_DIR="$SCRIPT_DIR/tdcs"

if [[ ! -f "$PCB_FILE" ]]; then
    echo "Error: $PCB_FILE not found"
    exit 1
fi

# Clean previous output
rm -rf "$OUTPUT_DIR"
mkdir -p "$OUTPUT_DIR"

echo "Generating gerber files..."
kicad-cli pcb export gerbers \
    --output "$OUTPUT_DIR/" \
    --layers "F.Cu,B.Cu,F.SilkS,B.SilkS,F.Mask,B.Mask,Edge.Cuts" \
    --subtract-soldermask \
    --use-drill-file-origin \
    "$PCB_FILE"

echo "Generating drill files..."
kicad-cli pcb export drill \
    --output "$OUTPUT_DIR/" \
    --format excellon \
    --drill-origin plot \
    --excellon-units mm \
    --generate-map \
    --map-format gerberx2 \
    "$PCB_FILE"

# Create zip for upload
echo "Creating zip archive..."
cd "$SCRIPT_DIR"
rm -f tdcs.zip
zip -j tdcs.zip tdcs/*

echo ""
echo "Output:"
echo "  Gerbers: $OUTPUT_DIR/"
echo "  Zip:     $SCRIPT_DIR/tdcs.zip"
echo ""
echo "Upload tdcs.zip to https://oshpark.com for fabrication."
