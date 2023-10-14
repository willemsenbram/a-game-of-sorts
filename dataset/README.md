# Interaction Data :performing_arts:

Dataset from the "[Collecting Visually-Grounded Dialogue with A Game Of Sorts](https://aclanthology.org/2022.lrec-1.242/)" paper.
The interactions can be reconstructed from the [JSON Lines](https://jsonlines.org/)-formatted files.

***

## Logs

Each line in `a-game-of-sorts_log_interaction_all.jsonl` represents a player action.
A player action is either a *message* or a *lock event*.
The message meta data includes the self-annotation.
Automatic unlocks following a misalignment between players locking images are also registered as lock events here.

### Example (sent message) :mag_right:

```json
{
    "interaction_id": "61c09b4ee90a3cc04fdce194", 
    "game_id": "game_1_dogs_1", 
    "board_id": "game_1_dogs_1_board_1", 
    "round_number": 1, 
    "round_active": true, 
    "message_number": 30, 
    "username": "tiny-elephant-9291", 
    "body_text": "Ok, how about the white curly dog. Looks like it has a strange haircut.", 
    "image_ids": [
        "n02093647_2585"
    ], 
    "timestamp": 1640013899727
}
```

| Name               | Type     | Description                                                                                                            |
|--------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **interaction_id** | _str_    | Interaction ID                                                                    |
| **game_id**        | _str_    | Game ID                                                                                               |
| **board_id**       | _str_    | Gameboard ID                                                                                          |
| **round_number**   | _int_    | Round number; starts at 0 if practice round, otherwise starts at 1                                |
| **round_active**   | _bool_   | Indicates whether the message was sent during (_true_) or after (_false_) a round                          |
| **message_number** | _int_    | Message number; resets each round, starts at 1                                                         |
| **username**       | _str_    | Username of the player that sent this message                                                                           |
| **body_text**      | _str_    | Text content of this message                                                                                            |
| **image_ids**      | _array_  | Array of image IDs (as _str_) that were selected by the player to indicate which images were referenced in the message: self-annotation |
| **timestamp**      | _int_    | Unix timestamp indicating the time at which the server received the message                                            |

### Example (lock event) :mag_right:

```json
{
    "interaction_id": "61bcbb1fe90a3cc04fda05de",
    "game_id": "game_3_pastries_1",
    "board_id": "game_3_pastries_1_board_1", 
    "round_number": 1, 
    "lock_event_number": 20,
    "username": "fabulous-chicken-6978", 
    "lock_event_type": "lock", 
    "image_id": "4446547654_dd68000444_o", 
    "timestamp": 1639759226835
}
```

| Name               | Type     | Description                                                                                                            |
|--------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **interaction_id** | _str_    | Interaction ID                                                                     |
| **game_id**        | _str_    | Game ID                                                                                               |
| **board_id**       | _str_    | Gameboard ID                                                                                          |
| **round_number**   | _int_    | Round number; starts at 0 if practice round, otherwise starts at 1                                |
| **lock_event_number** | _int_    | Lock event number; resets each round, starts at 1              |
| **username**          | _str_    | Username of the player that performed the action                                                                       |
| **lock_event_type**   | _str_    | Type of player action that was performed; 3 events are recognized: *lock*, *unlock automatic*, and *unlock manual*     |
| **image_id**          | _str_    | ID of the image on which the action was performed                                                                      |
| **timestamp**         | _int_    | Unix timestamp indicating the time at which the server registered the player action                                    |

***

## Board Mappings

Each line in `a-game-of-sorts_log_interaction_board_mappings.jsonl` represents the layout of the gameboard for a player for one round of an interaction.
Positions are numbered from left to right, top to bottom.

### Example (layout of the images on the gameboard for a single user for a single round) :mag_right:

```json
{
    "interaction_id": "61bcbb1fe90a3cc04fda05de", 
    "game_id": "game_3_pastries_1", 
    "board_id": "game_3_pastries_1_board_1", 
    "round_number": 1, 
    "username": "fabulous-chicken-6978", 
    "mapping": [
        {
            "position": 1, 
            "image_id": "4446547654_dd68000444_o"
        }, 
        {
            "position": 2, 
            "image_id": "3882682724_590c6b0deb_o"
        }, 
        {
            "position": 3, 
            "image_id": "15576048075_2bfcc378d9_o"
        }, 
        {
            "position": 4, 
            "image_id": "2112405187_bc8cd530e0_o"
        }, 
        {
            "position": 5, 
            "image_id": "4483886808_322e934cca_o"
        }, 
        {
            "position": 6, 
            "image_id": "6073742955_261d650954_o"
        }, 
        {
            "position": 7, 
            "image_id": "3963807163_8cff60a9a9_o"
        }, 
        {
            "position": 8, 
            "image_id": "5775603995_87c22a2bf5_o"
        }, 
        {
            "position": 9, 
            "image_id": "16373314089_5bcf18dbc5_o"
        }
    ]
}
```

| Name               | Type     | Description                                                                                                            |
|--------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **interaction_id** | _str_    | Interaction ID                                                                    |
| **game_id**        | _str_    | Game ID                                                                                               |
| **board_id**       | _str_    | Gameboard ID                                                                                          |
| **round_number**   | _int_    | Round number; starts at 0 if practice round, otherwise starts at 1                                |
| **username**         | _str_    | Username of the player to which the mapping belongs                                                                                   |
| **mapping**        | _array_  | Array of JSON objects where each object represents a visual stimulus and its position on the gameboard for this player for this round |
|                      |          |                                                                                                                                       |
| **position**         | _int_    | Position of the visual stimulus on the gameboard; starts at 1                                                |
| **image_id**         | _str_    | ID of the image                                                                                                                       |

***

## Game Configuration

Each line in `a-game-of-sorts_game_config.jsonl` represents the configuration of a gameboard for one game.

### Example (configuration of a single gameboard) :mag_right:

```json
{   
    "game_id": "game_1_dogs_1", 
    "board_number": 1,
    "board_id": "game_1_dogs_1_board_1", 
    "criterion": "You are planning to rob a bank. You have decided to bring your dog with you as your partner in crime. Which of these dogs would be most suitable to assist you in robbing the bank and why?", 
    "instruction": "Please discuss the scenario and come to an agreement on how to rank these dogs (starting with the dog that is most suitable) and motivate your choices!", 
    "image_ids": [
        "n02088238_13799", 
        "n02088364_12154", 
        "n02107683_1737", 
        "n02093647_2585", 
        "n02101556_7650", 
        "n02112137_11858", 
        "n02106030_14677", 
        "n02109961_5924", 
        "n02108915_2681"
    ]
}
```

| Name               | Type     | Description                                                                                                            |
|--------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **game_id**        | _str_    | Game ID                                                                                               |
| **board_number**   | _int_    | Default board number of this gameboard for this game (0 indicates practice round)                                      |
| **board_id**       | _str_    | Gameboard ID                                                                                          |
| **criterion**      | _str_    | Sorting criterion embedded in a short scenario                                                                         |
| **instruction**    | _str_    | Instruction that elaborates on what is expected from players this round                                                |
| **image_ids**      | _array_  | Array of image IDs (as _str_) that make up the visual stimuli of the gameboard for this game                           |

***

## Survey Configuration

Each line in `a-game-of-sorts_survey_config.jsonl` represents the configuration of one survey question in the post-game questionnaire.

### Example (configuration of a survey question) :mag_right:

```json
{
    "question_id": "q1", 
    "question_content": "Overall collaboration with my partner worked well.", 
    "question_type": "multiple_choice", 
    "answer_options": [ 
        { 
            "answer_id": "a", 
            "answer_content": "Strongly disagree" 
        }, 
        { 
            "answer_id": "b", 
            "answer_content": "Disagree" 
        }, 
        { 
            "answer_id": "c", 
            "answer_content": "Neither agree nor disagree" 
        }, 
        { 
            "answer_id": "d", 
            "answer_content": "Agree" 
        }, 
        { 
            "answer_id": "e", 
            "answer_content": "Strongly agree" 
        } 
    ] 
}
```

| Name                 | Type     | Description                                                                                                            |
|----------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **question_id**      | _str_    | Survey question ID                                                                                             |
| **question_content** | _str_    | Text content of the survey question or statement                                                                       |
| **question_type**    | _str_    | Survey question type, either *multiple_choice* or *open*                                          |
| **answer_options**   | _array_  | Array of JSON objects if **question_type** is *multiple_choice*; empty array if **question_type** is *open*            |
|                      |          |                                                                                                                        |
| **answer_id**        | _str_    | ID of the answer option (only applicable if **question_type** is *multiple_choice*)                                    |
| **answer_content**   | _str_    | Text content of the answer option (only applicable if **question_type** is *multiple_choice*)                          |

***

## Survey Answers (interaction-specific)

Each line in `a-game-of-sorts_survey_interaction_all.jsonl` represents the answers provided by a player to interaction-specific survey questions as part of the post-game questionnaire.

### Example (answers from a single user to interaction-specific survey questions) :mag_right:

```json
{
    "interaction_id": "61c09b4ee90a3cc04fdce194", 
    "game_id": "game_1_dogs_1",
    "username": "tiny-elephant-9291", 
    "answers": [
        {
            "answer": "e", 
            "question_id": "q1"
        }, 
        {
            "answer": "d", 
            "question_id": "q2"
        }, 
        {
            "answer": "d", 
            "question_id": "q3"
        }, 
        {
            "answer": "Interesting that humour also worked in this restricted format", 
            "question_id": "q10"
        }
    ]
}
```

| Name                 | Type     | Description                                                                                                            |
|----------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **interaction_id**   | _str_    | ID of the interaction for which the answers were provided                                                              |
| **game_id**          | _str_    | ID of the game for which the answers were provided                                                                     |
| **username**         | _str_    | Username of the player that provided the answers                                                                       |
| **answers**          | _array_  | Array of JSON objects where each object represents an answer provided to a specified survey question                   |
|                      |          |                                                                                                                        |
| **answer**           | _str_    | Answer to survey question provided by player                                                                           |
| **question_id**      | _str_    | ID of the survey question for which the answer was provided                                                            |

***

## Survey Answers (user overall)

Each line in `a-game-of-sorts_survey_user_all.jsonl` represents the answers provided by a player to general survey questions as part of the post-game questionnaire.

### Example (answers from a single user to general survey questions) :mag_right: 

```json
{   
    "username": "puny-badger-7135", 
    "answers": [
        {
            "answer": "a", 
            "question_id": "q4"
        }, 
        {
            "answer": "1997", 
            "question_id": "q5"
        }, 
        {
            "answer": "Spain", 
            "question_id": "q6"
        },
        {
            "answer": "Spanish", 
            "question_id": "q7"
        }, 
        {
            "answer": "a", 
            "question_id": "q8"
        }, 
        {
            "answer": "b", 
            "question_id": "q9"
        }, 
        {
            "answer": "", 
            "question_id": "q9-spec"
        }
    ]
}
```

| Name                 | Type     | Description                                                                                                            |
|----------------------|----------|------------------------------------------------------------------------------------------------------------------------|
| **username**         | _str_    | Username of the player that provided the answers                                                                       |
| **answers**          | _array_  | Array of JSON objects where each object represents an answer provided to a specified survey question                   |
|                      |          |                                                                                                                        |
| **answer**           | _str_    | Answer to survey question provided by player                                                                           |
| **question_id**      | _str_    | ID of the survey question for which the answer was provided                                                            |

***
***

# Images :camera:

For the data collection reported in our paper, we used five sets of nine images.
Each set represents a different image category: paintings, dogs, pastries, cars, and mobile phones.
The 45 images were taken from various sources.

***

### Paintings ([WikiArt](https://www.wikiart.org/))

| Image ID | Image | Info |
|----------|-------|------|
| adolphe-joseph-thomas-monticelli_italian-fishing-vessels-at-dusk | [View](https://uploads7.wikiart.org/images/adolphe-joseph-thomas-monticelli/italian-fishing-vessels-at-dusk.jpg) | [View](https://www.wikiart.org/en/adolphe-joseph-thomas-monticelli/italian-fishing-vessels-at-dusk) |
| albert-bierstadt_fishing-on-the-northwest-coast | [View](https://uploads7.wikiart.org/images/albert-bierstadt/fishing-on-the-northwest-coast.jpg) | [View](https://www.wikiart.org/en/albert-bierstadt/fishing-on-the-northwest-coast) |
| hans-hofmann_magnum-opus-1962 | [View](https://uploads7.wikiart.org/images/hans-hofmann/magnum-opus-1962.jpg) | [View](https://www.wikiart.org/en/hans-hofmann/magnum-opus-1962) |
| henri-edmond-cross_landscape | [View](https://uploads7.wikiart.org/images/henri-edmond-cross/landscape.jpg) | [View](https://www.wikiart.org/en/henri-edmond-cross/landscape) |
| ivan-aivazovsky_harbor-1850 | [View](https://uploads7.wikiart.org/images/ivan-aivazovsky/harbor-1850.jpg) | [View](https://www.wikiart.org/en/ivan-aivazovsky/harbor-1850) |
| paul-reed_14d-1964 | [View](https://uploads7.wikiart.org/images/paul-reed/14d-1964.jpg) | [View](https://www.wikiart.org/en/paul-reed/14d-1964) |
| paul-signac_the-bay-1906 | [View](https://uploads7.wikiart.org/images/paul-signac/the-bay-1906.jpg) | [View](https://www.wikiart.org/en/paul-signac/the-bay-1906) |
| sam-francis_falling-star-l-l249-1981 | [View](https://uploads7.wikiart.org/images/sam-francis/falling-star-l-l249-1981.jpg) | [View](https://www.wikiart.org/en/sam-francis/falling-star-l-l249-1981) |
| theo-van-rysselberghe_il-mediterraneo-presso-le-lavandou | [View](https://uploads7.wikiart.org/images/theo-van-rysselberghe/il-mediterraneo-presso-le-lavandou.jpg) | [View](https://www.wikiart.org/en/theo-van-rysselberghe/il-mediterraneo-presso-le-lavandou) |

***

### Dogs ([Stanford Dogs](http://vision.stanford.edu/aditya86/ImageNetDogs/))

| Image ID | Image | Info |
|----------|-------|------|
| n02088238_13799 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02088238-basset/n02088238_13799.jpg) | View |
| n02088364_12154 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02088364-beagle/n02088364_12154.jpg) | [View](https://www.dogbreedinfo.com/beagle.htm) |
| n02107683_1737 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02107683-Bernese_mountain_dog/n02107683_1737.jpg) | [View](https://www.flickr.com/photos/harttersinc/414159351/) |
| n02093647_2585 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02093647-Bedlington_terrier/n02093647_2585.jpg) | [View](https://www.flickr.com/photos/lucie8/18145348/) |
| n02101556_7650 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02101556-clumber/n02101556_7650.jpg) | [View](https://www.flickr.com/photos/caddydude672/4579983/) |
| n02112137_11858 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02112137-chow/n02112137_11858.jpg) | [View](https://www.flickr.com/photos/deridere/1399228857/) |
| n02106030_14677 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02106030-collie/n02106030_14677.jpg) | View |
| n02109961_5924 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02109961-Eskimo_dog/n02109961_5924.jpg) | [View](https://www.flickr.com/photos/amyhoney/362892325/) |
| n02108915_2681 | [View](http://vision.stanford.edu/aditya86/ImageNetDogs/images/n02108915-French_bulldog/n02108915_2681.jpg) | View |

***

### Pastries ([Open Images V6](https://storage.googleapis.com/openimages/web/download.html))

| Image ID | Image | Info |
|----------|-------|------|
| 15576048075_2bfcc378d9_o | [View](https://farm5.staticflickr.com/3932/15576048075_2bfcc378d9_o.jpg) | [View](https://www.flickr.com/photos/jamesonfink/15576048075) |
| 16373314089_5bcf18dbc5_o | [View](https://farm4.staticflickr.com/7438/16373314089_5bcf18dbc5_o.jpg) | [View](https://www.flickr.com/photos/picturesbyann/16373314089) |
| 2112405187_bc8cd530e0_o | [View](https://c1.staticflickr.com/3/2277/2112405187_bc8cd530e0_o.jpg) | [View](https://www.flickr.com/photos/amrufm/2112405187) |
| 3882682724_590c6b0deb_o | [View](https://farm3.staticflickr.com/3470/3882682724_590c6b0deb_o.jpg) | [View](https://www.flickr.com/photos/wordridden/3882682724) |
| 3963807163_8cff60a9a9_o | [View](https://c7.staticflickr.com/4/3451/3963807163_8cff60a9a9_o.jpg) | [View](https://www.flickr.com/photos/msvg/3963807163) |
| 4446547654_dd68000444_o | [View](https://c7.staticflickr.com/5/4071/4446547654_dd68000444_o.jpg) | [View](https://www.flickr.com/photos/jemimus/4446547654) |
| 4483886808_322e934cca_o | [View](https://farm3.staticflickr.com/2720/4483886808_322e934cca_o.jpg) | [View](https://www.flickr.com/photos/phn/4483886808) |
| 5775603995_87c22a2bf5_o | [View](https://farm5.staticflickr.com/5308/5775603995_87c22a2bf5_o.jpg) | [View](https://www.flickr.com/photos/stuartwebster/5775603995) |
| 6073742955_261d650954_o | [View](https://c1.staticflickr.com/7/6200/6073742955_261d650954_o.jpg) | [View](https://www.flickr.com/photos/12587661@N06/6073742955/) |

***

### Cars ([Open Images V6](https://storage.googleapis.com/openimages/web/download.html))

| Image ID | Image | Info |
|----------|-------|------|
| 14573636195_8be884e7a6_o | [View](https://farm5.staticflickr.com/3889/14573636195_8be884e7a6_o.jpg) | [View](https://www.flickr.com/photos/big-ashb/14573636195) |
| 15080160979_412c1f8fb6_o | [View](https://farm5.staticflickr.com/3925/15080160979_412c1f8fb6_o.jpg) | [View](https://www.flickr.com/photos/newgmparts/15080160979) |
| 15820279657_f4bd6c5bd2_o | [View](https://farm1.staticflickr.com/8651/15820279657_f4bd6c5bd2_o.jpg) | [View](https://www.flickr.com/photos/sg2012/15820279657) |
| 20582103526_efa0ed320e_o | [View](https://c2.staticflickr.com/1/641/20582103526_efa0ed320e_o.jpg) | [View](https://www.flickr.com/photos/monkey-kc/20582103526) |
| 3604858832_11ff8a52c3_o | [View](https://c5.staticflickr.com/4/3620/3604858832_11ff8a52c3_o.jpg) | [View](https://www.flickr.com/photos/supermac/3604858832) |
| 4109565917_7bd7a0c1c8_o | [View](https://farm3.staticflickr.com/2614/4109565917_7bd7a0c1c8_o.jpg) | [View](https://www.flickr.com/photos/stradablog/4109565917) |
| 4686234741_3a6a7b0b57_o | [View](https://c5.staticflickr.com/5/4044/4686234741_3a6a7b0b57_o.jpg) | [View](https://www.flickr.com/photos/12567713@N00/4686234741) |
| 5806423130_5b2b74f269_o | [View](https://c6.staticflickr.com/6/5106/5806423130_5b2b74f269_o.jpg) | [View](https://www.flickr.com/photos/daveseven/5806423130) |
| 6108067811_f969e78252_o | [View](https://c6.staticflickr.com/7/6201/6108067811_f969e78252_o.jpg) | [View](https://www.flickr.com/photos/50415738@N04/6108067811/) |

***

### Mobile phones ([Open Images V6](https://storage.googleapis.com/openimages/web/download.html))

| Image ID | Image | Info |
|----------|-------|------|
| 12517813753_7251a011c2_o | [View](https://farm6.staticflickr.com/5482/12517813753_7251a011c2_o.jpg) | [View](https://www.flickr.com/photos/karim2k/12517813753) |
| 2203610535_319a52d844_o | [View](https://farm1.staticflickr.com/2196/2203610535_319a52d844_o.jpg) | [View](https://www.flickr.com/photos/honou/2203610535) |
| 286956913_d1782e1586_o | [View](https://farm8.staticflickr.com/116/286956913_d1782e1586_o.jpg) | [View](https://www.flickr.com/photos/croco/286956913) |
| 2871935136_34dd9096c5_o | [View](https://c3.staticflickr.com/4/3054/2871935136_34dd9096c5_o.jpg) | [View](https://www.flickr.com/photos/8136496@N05/2871935136) |
| 3352759027_94cb468a1f_o | [View](https://c1.staticflickr.com/2/1029/3352759027_94cb468a1f_o.jpg) | [View](https://www.flickr.com/photos/whatleydude/3352759027) |
| 3368644533_56c4b2ac85_o | [View](https://farm4.staticflickr.com/3086/3368644533_56c4b2ac85_o.jpg) | [View](https://www.flickr.com/photos/brenbot/3368644533) |
| 3879107434_1502aa17a3_o | [View](https://c8.staticflickr.com/4/3496/3879107434_1502aa17a3_o.jpg) | [View](https://www.flickr.com/photos/morrissey/3879107434) |
| 5584312278_499a80a9cf_o | [View](https://farm8.staticflickr.com/5176/5584312278_499a80a9cf_o.jpg) | [View](https://www.flickr.com/photos/calgaryreviews/5584312278) |
| 8430496082_06d1b8fe00_o | [View](https://c8.staticflickr.com/9/8329/8430496082_06d1b8fe00_o.jpg) | [View](https://www.flickr.com/photos/edans/8430496082) |

***
***

## Download images

Running `get_images.sh` will first create a new directory `./images` in the current directory and then download the 45 images to it (requires `wget`):

```shell 
bash get_images.sh
``` 
