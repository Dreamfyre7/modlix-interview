# Challenge: Lossless String Compression

## Problem Statement

You need to implement a program that compresses a given input string losslessly and then decompresses it back to its original form.

## Requirements

- Write a function to compress a string.
- Write another function to decompress the compressed output.
- Ensure that decompress(compress(s)) == s for all valid inputs.
- The compression should be lossless, meaning no data should be lost.

## Constraints

- The input string will contain only alphanumeric characters (a-z, A-Z, 0-9).
- The implementation should not use standard compression libraries.
- The solution should work efficiently for large strings (100,000+ characters).

## Bonus Challenges (Optional)

1. Support Unicode characters. I.e. input string can contain any Unicode characters.
2. Implement a different lossless compression algorithm (e.g., Huffman coding).
                                           
public class StringCompression {

    public static String compress(String s) {
        if (s == null || s.isEmpty()) return "";

        StringBuilder compressed = new StringBuilder();
        int count = 1;

        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) {
                count++;
            } else {
                compressed.append(s.charAt(i - 1)).append(count);
                count = 1;
            }
        }
        compressed.append(s.charAt(s.length() - 1)).append(count);

        return compressed.toString();
    }

    // Decompress function to restore original string
    public static String decompress(String s) {
        if (s == null || s.isEmpty()) return "";
        StringBuilder decompressed = new StringBuilder();
        int i = 0;
        while (i < s.length()) {
            char character = s.charAt(i++);
            int count = 0;
            while (i < s.length() && Character.isDigit(s.charAt(i))) {
                count = count * 10 + (s.charAt(i) - '0');
                i++;
            }
            decompressed.append(String.valueOf(character).repeat(count));
        }
        return decompressed.toString();
    }

    public static void main(String[] args) {
        String original = "aaabbbcccddeeeffff";
        String compressed = compress(original);
        String decompressed = decompress(compressed);
        System.out.println("Original: " + original);
        System.out.println("Compressed: " + compressed);
        System.out.println("Decompressed: " + decompressed);
        System.out.println("Lossless: " + original.equals(decompressed));
    }
}
