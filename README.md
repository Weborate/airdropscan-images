## AirdropScan Images

**Important:** Do NOT rename/move images in this repo. The file names are used on the website.

### Resize images:

Install imagemagick

```
mkdir -p /path_to/airdropscan-images/tokens/70

for ext in jpg jpeg png webp; do
  for img in /path_to/airdropscan-images/tokens/original_size/*.$ext; do
    if [ -f "$img" ]; then
      # Get the dimensions of the image
      dimensions=$(magick identify -format "%wx%h" "$img")
      width=$(echo $dimensions | cut -d'x' -f1)
      height=$(echo $dimensions | cut -d'x' -f2)

      # Determine the size of the square crop (smallest dimension of the image)
      size=$(( width < height ? width : height ))

      # Calculate the offset to crop from the center
      x_offset=$(( (width - size) / 2 ))
      y_offset=$(( (height - size) / 2 ))

      # Crop the square from the center and resize to 70x70 pixels
      magick "$img" -crop "${size}x${size}+${x_offset}+${y_offset}" -resize 70x70 "/path_to/airdropscan-images/tokens/70/$(basename "$img")"
    fi
  done
done

```
