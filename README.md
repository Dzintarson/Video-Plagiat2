# Video-Plagiat2
Analis video2
# Code for Video Plagiarism Analyzer using video hashing
import imagehash
from moviepy.editor import VideoFileClip

def calculate_video_similarity(video_path1, video_path2, threshold=5):
    # Extract frames from the videos
    frames1 = extract_frames(video_path1)
    frames2 = extract_frames(video_path2)

    # Calculate the average hash for each video
    hash1 = average_video_hash(frames1)
    hash2 = average_video_hash(frames2)

    # Calculate the Hamming distance between the hashes
    hamming_distance = hash1 - hash2

    # Check if the Hamming distance is below the threshold
    if hamming_distance < threshold:
        return True
    else:
        return False

def extract_frames(video_path):
    # Extract frames from the video using moviepy
    video_clip = VideoFileClip(video_path)
    frames = [frame for frame in video_clip.iter_frames(fps=1)]
    return frames

def average_video_hash(frames):
    # Calculate the average hash for a list of frames
    hashes = [imagehash.average_hash(frame) for frame in frames]
    average_hash = sum(hashes) / len(hashes)
    return average_hash

# Example usage
video_path1 = "path/to/your/video1.mp4"
video_path2 = "path/to/your/video2.mp4"

if calculate_video_similarity(video_path1, video_path2):
    print("Plagiarism detected!")
else:
    print("No plagiarism found.")
