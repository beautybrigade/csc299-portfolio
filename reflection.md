# Reflection

## 1. What a fresh session asked about that was already settled

One example of a fresh session asking about something that was already settled was in round 3 of the project's further development. In round 2, I had decided to keep both the terminal game and the browser game, and when I began to make the next requirements for round 3, the assistant asked me again if the terminal version of the game should also receive the same changes that the web version of round 3 would receive. The repository was missing a standing rule about this. My round 2 choice was only recorded in spec.md, not in CLAUDE.md, so the new session did not know it applied to every round. In order to prevent the questions from continuously occurring, I added rule 8 to CLAUDE.md stating that every change applies to both versions (commit 280ea65).

## 2. The round that changed an earlier requirement

In round 3, I changed an earlier requirement, R3, that I had made in the initial requirements. The change included that for pedicure services, the game should include an animation of a foot soak, similar to that of washing hands in a manicure service. This caused two tests to break, specifically located in tests/test_r4_steps.py. The two stopped passing because they listed the exact steps for a stand-alone pedicure service and a combo service, and those didn't include the new foot wash step. The tests caught it. The new tests were written first (commit 91c2ffe), and the two old tests failed until they were updated to include the foot wash. Decision record 0005 explains the change for someone who was not there, including why R3 changed, the other options I considered, and which tests actually had to change.

## 3. A test that checked nothing useful

A test that didn't check anything useful was located in tests/test_r8_animation.py. The test test_r8_stylesheet_has_keyframes_for_each_step_animation opens the style file and checks that the words "@keyframes file", "@keyframes buff", and so on appear in it. 

The key line is:

    assert f"@keyframes {name}" in css

The check is basically not useful because an animation could be empty, broken, or look completely wrong, and the test would still pass, as long as the name is written in the file. Decision record 0002 admits this as well. This kind of test also missed that the Polish button was plain grey from round 3 until round 4, when the assistant noticed it.

## 4. A commit I would write differently

One commit that I would write differently is 8339aa0 in nail-salon-tycoon. This commit's message, "spec: state that the player is told if a client has old product on", says what changed but doesn't explain why. I would rewrite it as something like "spec: state that the player is told if a client has old product on, so the player knows to start with product removal".

## 5. A function I didn't read while building

One function that I didn't read while building was finish_service in salon.py. I believe this code takes the number of mistakes and checks how many were made. If the number of mistakes is zero, the player earns a star. If the number of mistakes is equal to one, the price of the service is divided by 2 and the player only earns half of the service price. If the number of mistakes isn't zero or one, the player doesn't earn any money for the service. Once the code is run, the program returns the stats for the client serviced.

When I asked an assistant, it said the function judges one finished service: it gets the number of mistakes from count_mistakes(), then gives 1 star and full price for 0 mistakes, half a star and half price for 1, and nothing for 2 or more. I got the main idea right: how the pay changes with 0, 1, or more mistakes. What I missed was that the function doesn't count the mistakes itself, that 0 mistakes also pays the full price, that 1 mistake gives half a star, and that a client only counts as "satisfied" with 0 mistakes.