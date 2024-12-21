# Python-Projects

import json
def load_data():
    try:
        with open('youtube.txt','r') as file:
            test = json.load(file)
            print(type(test))
            return test
    except FileNotFoundError:
        return []

def save_data_helper(videos):
    with open('youtube.txt','w') as file:
        json.dump(videos, file)
def list_all_videos(videos):
    for index, video in enumerate(videos, start =1):
        print("\n")
        print("*" * 70)
        print(f"{index}. {video['name']}, duration: {video['time']}")
def add_videos(videos):
    name = input("enter video name")
    time = input("enter your time")
    videos.append({"name":name, "time":time})
    save_data_helper(videos)

def update_videos(videos):
    list_all_videos(videos)
    index = int(input("enter index"))
    if 1 <= index <= len(videos):
        name = input("enter video name")
        time = input("enter your time")
        videos[index-1] = {'name':name, 'time':time}
        save_data_helper(videos)
    else:
        print("invalid index")
def remove_videos(videos):
    list_all_videos(videos)
    index = int(input("enter the video to be deleted"))
    if 1 <= index <= len(videos):
        del videos[index-1]
        save_data_helper(videos)
    else:
        print("invalid video index")
def main():

    videos = load_data()
    while True:
        print("\n youtube manager | choose an option")
        print("\n 1. list your fav videos")
        print("\n 2. add a youtube video")
        print("\n 3. update a youtube video")
        print("\n 4. remove a youtube video")
        print("\n 5. exit the program")
        choice = input("Enter your choice: ")
        print(videos)

        match choice:
            case "1":
                list_all_videos(videos)
            case "2":
                add_videos(videos)
            case "3":
                update_videos(videos)
            case "4":
                remove_videos(videos)
            case "5":
                break
            case _:
                print("Invalid choice")

if __name__ == "__main__":
    main()
