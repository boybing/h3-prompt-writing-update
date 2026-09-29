---

name: h3-prompt-writing
description: Write high-control MiniMax H3 video generation prompts for T2VA, I2VA, FL2VA, L2VA, and Ref2VA. Use when converting stories, scripts, dialogue, reference images, keyframes, and director instructions into structured H3 prompts with character continuity, spatial blocking, camera direction, shot scale, natural camera movement, dialogue control, emotional acting, reference-image grounding, temporal continuity, and Chinese/English prompt outputs.
compatibility: Portable to any agent that can read local files — no external API calls, MiniMax Hub tools, or proprietary runtime required. The agents/openai.yaml file only adds optional ChatGPT/Codex UI metadata; it does not restrict the skill to OpenAI agents.

H3 Prompt Writing

1. Mission

The primary objective is NOT to make prompts longer or more cinematic.

The primary objective is:

«Preserve the user's intended characters, actions, dialogue, spatial relationships, emotional performance, references, timing, camera language, and continuity with the fewest unnecessary assumptions.»

Act as a film director + cinematographer + continuity supervisor + H3 prompt compiler.

Convert the user's story or shot request into a precise H3 generation prompt while avoiding unnecessary invention.

The final prompt should feel like a director's executable shot plan rather than a literary story summary.

---

2. Workflow

Follow this pipeline:

1. Identify the input mode:
   
   - T2VA
   - I2VA
   - FL2VA
   - L2VA
   - Ref2VA

2. Read the appropriate official structure:
   
   - Base modes → "references/base-en.txt"
   - Full-reference mode → "references/ref-en.txt"

3. Parse the user's request into:
   
   - Character Registry
   - Reference Registry
   - Speaker Registry
   - Spatial Blocking
   - Action Plan
   - Emotional Performance
   - Dialogue
   - Camera Plan
   - Shot Scale
   - Sound Plan
   - Timeline

4. Lock continuity constraints before writing the visual description.

5. Plan the shot using director logic.

6. Compile the shot into the official H3 prompt structure.

7. Run the Consistency Audit.

8. If contradictions are found, silently rewrite the prompt before output.

9. Output:
   
   - Chinese version
   - English version

Do not expose the internal analysis unless explicitly requested.

---

3. Official H3 Structure

Always preserve the official H3 section structure required by the selected mode.

For base modes, use:

- "integrated_multimodal_description"
- "overall_soundscape"
- "non_diegetic_music"

For full-reference Ref2VA, use:

- "subject_definitions"
- "summary"
- "retention_analysis"
- "detailed_description"
- "overall_soundscape"
- "non_diegetic_music"

Do not casually rename, reorder, or remove official fields.

Read the corresponding reference guide before compiling the final prompt.

---

4. Language Rules

4.1 Internal Generation Logic

Think in terms of:

- who
- where
- position
- orientation
- action
- emotional state
- dialogue
- who is speaking
- who is listening
- camera position
- camera direction
- shot size
- camera movement
- cut timing
- sound
- continuity

4.2 Output

Always provide two complete versions:

1. 中文提示词
2. English Prompt

The Chinese version should be natural and directly usable.

The English version should preserve the exact same:

- character identities
- positions
- directions
- actions
- emotions
- dialogue
- timing
- camera movement
- shot structure
- sound design

Do NOT introduce new content when translating from Chinese to English.

---

5. Hard Constraints

The following constraints have priority over stylistic decoration.

Priority order:

1. Character identity
2. Character count
3. Character spatial position
4. Character orientation
5. Character relationship
6. Physical action
7. Dialogue and speaker identity
8. Emotional performance
9. Object interaction
10. Camera direction
11. Shot scale
12. Camera movement
13. Editing / cut
14. Environment
15. Lighting
16. Style / visual decoration

Never sacrifice character identity, position, action, dialogue, or continuity merely to make the scene more cinematic.

---

6. Character Registry

Create a stable identity for every important reusable character.

Use:

- "<Subject 1>"
- "<Subject 2>"
- "<Subject 3>"

A character must keep the same Subject ID throughout the prompt and across connected shots.

Example:

"<Subject 1>" = main male character

"<Subject 2>" = main female character

Do not switch identifiers halfway through a scene.

---

7. Character Count Lock

When multiple people are visible, explicitly control the number of physical characters.

Example:

«Exactly two human characters are visible in this shot: "<Subject 1>" and "<Subject 2>".»

Do not introduce:

- duplicate characters
- clones
- accidental background versions
- extra people
- duplicated limbs
- additional speaking characters

unless explicitly requested.

---

8. One Subject = One Physical Entity

Each Subject ID represents exactly one physical character.

Never interpret:

- reference image
- reflection
- memory
- imagined figure
- visual resemblance

as an additional physical character unless explicitly requested.

If a reflection is necessary, clearly identify it as a reflection of the existing Subject rather than a second person.

---

9. Unrequested Entity Control

Do not introduce unnecessary:

- people
- animals
- vehicles
- weapons
- props
- background characters
- objects
- signs
- text
- creatures

If the user did not request an entity and it is not necessary for the shot, do not invent it.

---

10. Reference Registry

Maintain a clear reference registry.

Examples:

- "<Picture 1>" = "<Subject 1>" character reference
- "<Picture 2>" = hand reference
- "<Picture 3>" = tail reference
- "<Picture 4>" = background reference

Keep labels identical throughout the entire prompt.

---

11. Reference Images Control Appearance Description

When a reference image already defines a character's appearance, DO NOT unnecessarily rewrite the character's physical appearance or clothing.

Do not redundantly describe:

- hair color
- facial features
- body shape
- clothing
- shoes
- accessories
- detailed costume design

if these are already clearly established by the reference image.

Instead, identify the character by Subject ID and reference.

Example:

«"<Subject 1>" follows "<Picture 1>" for identity and appearance.»

Focus the prompt on:

- position
- orientation
- action
- expression
- dialogue
- interaction
- camera
- continuity

Important Exception

Only describe appearance or clothing when necessary to:

1. distinguish two characters;
2. specify an intentional wardrobe change;
3. clarify a visual property not present in the reference;
4. preserve continuity when the user explicitly provides the detail.

Do not repeatedly restate reference-defined appearance.

---

12. Reference Asset Is Not Automatically a Physical Object

A reference image is a source of visual information.

It does NOT automatically become an object or person physically appearing in the generated video.

For example:

«"<Picture 1>" is a character reference only and must NOT appear as a separate image, photograph, panel, or object in the final video.»

This rule applies unless the user explicitly requests the reference itself to appear.

---

13. Spatial Blocking

Every important multi-character shot should define character blocking.

Describe:

- left / right
- front / back
- near / far
- center
- foreground / background
- relative distance
- relative position
- movement direction

Example:

«"<Subject 1>" stands on the left side of the frame.
"<Subject 2>" stands on the right side of the frame.
"<Subject 1>" remains slightly closer to camera than "<Subject 2>".»

Do not rely only on names.

---

14. Character Orientation

Every important character should have a clear facing direction when relevant.

Examples:

- facing "<Subject 2>"
- looking toward the doorway
- facing camera
- facing screen left
- facing screen right
- body oriented toward "<Subject 1>" while eyes remain on "<Subject 1>"

Do not leave character orientation ambiguous in dialogue scenes.

---

15. Relative Position Lock

Once the spatial relationship is established, maintain it across connected shots unless the script explicitly changes it.

Example:

«"<Subject 1>" remains on the left and "<Subject 2>" remains on the right throughout the conversation unless a later action explicitly changes their positions.»

Do NOT randomly swap their positions between cuts.

If a character moves, describe:

1. starting position
2. movement direction
3. destination
4. new relative position

---

16. Speaker Registry

Assign stable speaker IDs.

Example:

- "(S1)" → "<Subject 1>"
- "(S2)" → "<Subject 2>"

A speaker ID must never change.

---

17. Dialogue Format

Use:

"<d>[Language] exact spoken words</d>"

Example:

"(S1) <d>[Chinese] 你到底想干什么？</d>"

The dialogue must remain exactly as provided unless the user asks for rewriting.

---

18. Dialogue Is Audio, Not Visible Text

Dialogue is spoken audio.

By default:

«The spoken dialogue is audible speech only. No subtitles, captions, speech bubbles, floating dialogue text, or other visible text representing the spoken words appear on screen.»

Do not generate subtitles automatically.

Only include visible text when the user explicitly requests it.

---

19. Silent Character Rule

A character MUST NOT speak unless the user explicitly assigns speech or a vocal action to that character.

Silence is an intentional state.

If a character has no dialogue:

«"<Subject 2>" remains silent.»

Do not invent:

- dialogue
- muttering
- whispering
- laughing
- sighing
- shouting
- emotional vocalizations

unless appropriate and explicitly authorized.

---

20. Silent Mouth Behavior

For silent characters:

«The character remains silent with a naturally closed or relaxed mouth, reacting through subtle facial expression and eye movement rather than speaking.»

Avoid random:

- lip movement
- mouth opening
- lip-sync behavior
- talking gestures

when the character is not speaking.

---

21. Speech Authorization

Only the currently authorized speaker may speak.

Example:

«"(S1)" speaks.
"(S2)" listens silently.»

Do not allow "<Subject 2>" to accidentally speak during "<Subject 1>"'s dialogue.

---

22. Eye Contact During Dialogue

When two or more principal characters are talking to each other:

«The active speaker's eyes naturally look toward the other principal character while speaking.»

The listening character should also naturally look toward the active speaker unless the script explicitly requires another gaze direction.

Avoid:

- staring randomly into camera
- looking away without reason
- looking at an unrelated background object
- talking while visually ignoring the other character

Important

Eye direction should follow the established spatial relationship.

If "<Subject 1>" is on screen left and "<Subject 2>" is on screen right:

- "<Subject 1>" generally looks toward screen right / "<Subject 2>"
- "<Subject 2>" generally looks toward screen left / "<Subject 1>"

unless the script specifies otherwise.

---

23. Turn-Taking

Dialogue should follow natural conversational turn-taking.

Example:

1. "<Subject 1>" speaks.
2. "<Subject 2>" listens silently.
3. "<Subject 1>" finishes.
4. "<Subject 2>" responds.

Do not overlap dialogue unless explicitly requested.

---

24. No Dialogue Fabrication

Never invent dialogue merely because the character:

- looks angry
- looks surprised
- reacts emotionally
- moves toward another person
- opens their mouth
- gestures

If no words are provided, do not create words.

---

25. Emotional Performance

Characters must NOT behave like static mannequins.

When dialogue or action carries emotion, translate the emotion into visible acting.

Avoid vague instructions such as:

«He is angry.»

Prefer observable performance:

«"<Subject 1>" tightens his eyebrows, fixes an intense gaze on "<Subject 2>", and says angrily...»

or:

«"<Subject 1>" pauses briefly, narrows his eyes, then gives a subtle, sly smile before speaking.»

Use combinations of:

- eyebrow movement
- eye movement
- gaze
- facial tension
- mouth expression
- head movement
- posture
- hand gestures
- body movement
- breathing
- pauses
- changes in physical distance

Do not overuse exaggerated facial acting.

The goal is natural, believable human performance.

---

26. Emotional Action Binding

Emotion should be attached to an observable action.

Bad:

«He is very angry.»

Better:

«He furrows his brows, leans slightly forward, and speaks with controlled anger.»

Bad:

«She is sinister.»

Better:

«She pauses, raises one corner of her mouth into a subtle, sly smile, and calmly looks directly at him.»

The emotional state should be visible through behavior.

---

27. Action Priority

When several actions compete within one short shot, prioritize the user's primary action.

Use:

«Primary action → supporting reaction → camera response»

Do not overload one shot with too many independent actions.

---

28. Action Atomicity

Break complicated actions into understandable sequential units.

Example:

«He turns his head → locks eyes with her → furrows his brows → speaks → pauses → suddenly steps aside.»

Avoid compressing too many unrelated actions into one vague sentence.

---

29. One Shot = One Primary Action

For short H3 clips, each shot should normally have one dominant physical action.

Secondary reactions are allowed.

Do not force:

- walking
- fighting
- talking
- turning
- sitting
- picking up objects
- camera rotation
- zoom
- environmental transformation

all into the same moment unless the user explicitly requests them.

---

30. Director's Camera Thinking

The prompt should use actual filmmaking logic rather than simply describing a moving camera.

For every important shot consider:

1. Where is the camera?
2. Which direction is the camera facing?
3. What is the shot size?
4. What is the subject of attention?
5. Why does the camera move?
6. When should the shot cut?
7. What visual information should the next shot reveal?

Use camera movement naturally.

Avoid unnecessary:

- constant zooming
- random orbiting
- excessive camera shaking
- arbitrary camera rotation
- dramatic movement without narrative purpose

---

31. Camera Direction

Explicitly define camera orientation when it matters.

Examples:

- camera faces "<Subject 1>"
- camera faces the two characters from a three-quarter angle
- camera looks toward the doorway
- camera is positioned behind "<Subject 1>" and faces "<Subject 2>"
- camera moves from screen left toward screen right

Do not leave camera direction ambiguous in important dialogue or action shots.

---

32. Shot Scale

Use appropriate cinematic shot sizes.

Common shot scales:

- Extreme Wide Shot (EWS)
- Wide Shot (WS)
- Full Shot (FS)
- Medium Full Shot (MFS)
- Medium Shot (MS)
- Medium Close-Up (MCU)
- Close-Up (CU)
- Extreme Close-Up (ECU)

Choose shot size according to narrative purpose.

Wide Shot

Use for:

- geography
- establishing spatial relationships
- body movement
- environmental context

Medium Shot

Use for:

- dialogue
- gestures
- interaction
- body language

Close-Up

Use for:

- important emotional reactions
- eyes
- facial tension
- critical dialogue moments

Do not switch shot sizes randomly.

---

33. Natural Camera Movement

Use camera movement as a director would.

Examples:

- slow dolly in during an emotionally important line
- gentle tracking shot following a character
- subtle push-in when tension increases
- restrained pan following a character's movement
- static framing when dialogue performance is more important than camera movement

Camera movement should support:

- character emotion
- action
- spatial information
- story emphasis

not compete with them.

---

34. Cutting / Shot Transition Logic

Cuts must have a reason.

Prefer cuts based on:

- completion of a line
- completion of an action
- change of subject attention
- important reaction
- reveal
- change of spatial information
- emotional emphasis

Avoid arbitrary cutting in the middle of important dialogue unless intentionally requested.

---

35. Dialogue Completion Before Scenic Cut

When a character is delivering an important line, allow the line to finish before cutting to a scenic or environmental shot unless the user explicitly requests an interruption.

Preferred structure:

«"<Subject 1>" completes the sentence → natural reaction / pause → cut to environmental or scenic shot.»

Do NOT cut away halfway through an important sentence simply to show scenery.

---

36. Scenic Cutaways

When using scenery or environmental cutaways:

- place them at a natural narrative boundary;
- preferably after a character finishes speaking;
- preserve the dialogue timing;
- use the scenic shot to provide atmosphere, geography, or emotional breathing room.

Example:

«"<Subject 1>" finishes speaking. A brief natural pause follows. Cut to a wide shot of the surrounding landscape.»

---

37. Natural Transition Buffer

For each logical shot or dialogue segment, preserve approximately 0.5 seconds of natural visual continuity at the end when the total duration allows.

The 0.5-second buffer is NOT a separate artificial blank period.

It should contain natural:

- facial reaction
- breathing
- body settling
- eye movement
- subtle gesture
- environmental motion
- camera settling
- natural continuation of the action

Example for a 10-second video:

«Dialogue occupies approximately 5 seconds → the speaker completes the line → approximately 0.5 seconds of natural reaction / visual continuity → then transition to the next shot.»

Do NOT simply freeze the character for 0.5 seconds.

Do NOT mechanically add 0.5 seconds after every sentence if this would exceed the requested total duration.

The entire timeline must still fit the requested video length.

---

38. Timeline Control

Every action and dialogue must fit inside the requested duration.

For a 10-second video:

- do not create a 12-second description;
- do not give dialogue more time than physically possible;
- do not insert unnecessary pauses;
- reserve transition buffers only when timing permits.

When dialogue is long, prioritize:

1. exact dialogue
2. natural speech timing
3. primary action
4. reaction
5. camera transition

Do not sacrifice exact dialogue merely to add decorative camera movement.

---

39. Spatial Continuity Across Cuts

When cutting between camera angles, maintain the established spatial relationship.

Use consistent screen direction.

Example:

«"<Subject 1>" remains screen left and "<Subject 2>" remains screen right across the conversation.»

Unless a deliberate camera-axis change is requested, avoid unintentionally reversing their positions.

Maintain:

- left/right relationship
- front/back relationship
- relative distance
- facing direction
- eye-line
- screen direction

---

40. 180-Degree / Axis Awareness

For two-person dialogue scenes, maintain a consistent camera side of the interaction whenever practical.

Do not randomly cross the conversational axis.

If an axis crossing is intentionally required, make it explicit and use a motivated transition.

The purpose is to preserve spatial clarity and prevent characters from appearing to suddenly swap positions.

---

41. Wardrobe Continuity

When clothing is established by a reference image or previous shot:

- preserve it;
- do not randomly change it;
- do not invent additional accessories;
- do not alter colors or style.

If the user explicitly requests a wardrobe change, mark it as an intentional state transition.

---

42. Prop Ownership

Every important prop should have a clear owner.

Example:

«The knife remains in "<Subject 1>"'s right hand.»

Do not allow props to:

- teleport
- switch owners
- duplicate
- disappear without cause
- change hand randomly

Track prop state across shots.

---

43. Temporal Continuity

Track the following across connected shots:

- identity
- character count
- appearance
- wardrobe
- hairstyle
- accessories
- spatial position
- orientation
- gaze direction
- held objects
- object ownership
- action state
- emotional state
- speaker state
- camera relationship

Only change a state when the script explicitly causes the change.

---

44. Environment Continuity

Do not randomly change:

- location
- time of day
- weather
- lighting direction
- major background elements

unless the script requires it.

When cutting to scenery, ensure it belongs to the same narrative environment unless the user explicitly requests a location change.

---

45. No Background Music by Default

Unless the user explicitly requests background music:

«There is NO non-diegetic background music.»

Use:

- dialogue
- environmental ambience
- footsteps
- clothing movement
- object sounds
- natural environmental sounds

when appropriate.

Do not automatically add cinematic music.

For the "non_diegetic_music" field, explicitly state that no background music is used unless the user requests otherwise.

---

46. Sound Design

Sound should support the visual action.

Use natural diegetic sound where appropriate:

- footsteps
- door movement
- wind
- rain
- room ambience
- object impacts
- cloth movement
- breathing
- environmental sounds

Do not create unnecessary sound effects.

Dialogue remains the highest-priority intentional vocal content.

---

47. Non-Speech Vocalization

Do not automatically add:

- sighs
- gasps
- groans
- laughter
- cries
- grunts

unless explicitly requested or clearly necessary for a specified action.

If uncertain:

«KEEP THE CHARACTER SILENT.»

---

48. Singing

Singing is treated as explicit vocal action.

If the user requests singing:

- identify the singer;
- specify the exact lyrics;
- preserve language;
- prevent other characters from accidentally singing;
- synchronize singing with the requested action and timing.

Do not convert ordinary dialogue into singing.

---

49. Off-Screen Voice

If a voice belongs to a character who is not visible:

Clearly specify:

«"(S1)" speaks off-screen.»

Do not create a visible duplicate of the off-screen character unless requested.

---

50. Keyframe Rules

For I2VA / FL2VA / L2VA:

- explicitly connect the first frame and/or last frame to the timeline;
- preserve the supplied keyframe's spatial and visual information;
- do not introduce contradictory character positions;
- do not arbitrarily change character identity or wardrobe.

For FL2VA:

«describe the continuous visual and physical path between the first and last frame.»

For L2VA:

«build a plausible transition toward the supplied last frame.»

---

51. Full-Reference / Ref2VA Rules

Ref2VA must clearly distinguish:

1. reference identity
2. retained visual information
3. physical subjects
4. generated motion
5. scene environment

Reference labels must remain stable.

Do not allow a reference image to become a separate physical entity.

---

52. Reference Retention

When reference images are supplied, preserve the information the user intends to retain.

Examples:

- character identity
- hand structure
- tail
- background
- environment
- object design

Do not unnecessarily copy unrelated information from a reference.

---

53. Prompt Adherence Compiler

Before finalizing the prompt, convert the user's natural-language request into explicit constraints.

Example:

User:

«男的在左边，女的在右边，男的看着女的说话。»

Compiler:

«"<Subject 1>" remains on screen left.
"<Subject 2>" remains on screen right.
"<Subject 1>" faces and looks toward "<Subject 2>" while speaking.»

Do not leave critical spatial or behavioral information implicit.

---

54. Director Thinking Layer

Before generating the final prompt, ask internally:

Blocking

- Where is each character?
- Who is closer to camera?
- Who is in foreground/background?
- Which direction is each character facing?

Performance

- Who speaks?
- Who listens?
- Where are the eyes looking?
- What emotion is visible?
- What facial or body action expresses that emotion?

Camera

- What is the camera position?
- What direction is it facing?
- What is the shot size?
- Should the camera be static, tracking, panning, dollying, or pushing in?
- Why does the camera move?

Editing

- When should the shot cut?
- Has the important dialogue finished?
- Has the primary action finished?
- Does the next shot provide useful information?

Continuity

- Are left/right positions preserved?
- Are character identities preserved?
- Are props preserved?
- Are wardrobe and appearance preserved through references?
- Is the eye-line consistent?

Sound

- Is there dialogue?
- Is there environmental sound?
- Is background music explicitly requested?

---

55. Minimize Uncontrolled Interpretation

Do not use excessive poetic language that gives H3 too much freedom.

Avoid:

«A mysterious and emotionally complex cinematic moment full of indescribable tension.»

Prefer:

«"<Subject 1>" pauses, furrows his brows, looks directly at "<Subject 2>", then speaks in a controlled but angry tone.»

Use observable, executable descriptions.

---

56. Avoid Redundant Appearance Description

If a reference image already establishes:

- face
- hairstyle
- clothing
- body shape
- accessories

do not repeat those descriptions throughout every shot.

Use the reference as the identity anchor.

Spend prompt space on:

- blocking
- action
- emotion
- dialogue
- camera
- continuity

---

57. Final Consistency Audit

Before output, verify:

Character

- Is every character assigned a stable Subject ID?
- Is the character count correct?
- Are there accidental duplicates?
- Are there unnecessary people?

Spatial

- Is each important character's position clear?
- Is each character's orientation clear?
- Are relative positions preserved?
- Is screen direction consistent?

Dialogue

- Is every line assigned to the correct speaker?
- Are silent characters actually silent?
- Are speakers looking toward the person they are addressing?
- Is dialogue represented as audio rather than subtitles?

Acting

- Is the emotional state expressed through visible behavior?
- Are characters avoiding a wooden / expressionless performance?
- Are actions and emotions synchronized?

Camera

- Is camera direction clear?
- Is shot scale appropriate?
- Is camera movement motivated?
- Are cuts motivated?
- Are important lines allowed to finish before scenic cutaways?

Continuity

- Are wardrobe and appearance preserved?
- Are props preserved?
- Is object ownership preserved?
- Are positions preserved?
- Are references used correctly?

Sound

- Is background music absent unless explicitly requested?
- Is environmental sound appropriate?
- Are unnecessary vocalizations avoided?

Timeline

- Does everything fit the requested duration?
- Is there natural transition time?
- Is approximately 0.5 seconds of natural continuity preserved where practical?
- Are there unnecessary pauses?

---

58. Default Anti-Artifact Block

Unless the user explicitly requests otherwise, enforce:

«No duplicate characters. No cloned people. No accidental extra characters. No random dialogue. No unrequested speech. No subtitles or captions. No speech bubbles. No floating dialogue text. No random text. No character position swapping. No unexplained wardrobe changes. No prop teleportation. No random prop duplication. No unnatural lip movement for silent characters. No random camera spinning. No unnecessary zooming. No arbitrary cuts. No background music unless explicitly requested.»

Use structural constraints first.

Do not rely only on negative prompts.

---

59. Do Not Overuse Negative Prompts

Negative constraints are useful, but they should not replace positive instructions.

Prefer:

«"<Subject 2>" listens silently and looks toward "<Subject 1>".»

over only:

«No talking.»

Prefer:

«Exactly two characters are visible: "<Subject 1>" and "<Subject 2>".»

over only:

«No extra people.»

Positive structural grounding is generally preferred.

---

60. Do Not Overload the Prompt

The goal is NOT maximum prompt length.

If two rules express the same constraint, combine them.

Remove:

- repeated appearance descriptions
- repeated environment descriptions
- redundant adjectives
- unnecessary cinematic language
- duplicated negative prompts

Keep the information that controls H3's behavior.

---

61. Shot Construction Template

For each shot, internally construct:

«TIME → SUBJECTS → POSITION → ORIENTATION → PRIMARY ACTION → EMOTION → DIALOGUE → GAZE → CAMERA POSITION → CAMERA DIRECTION → SHOT SCALE → CAMERA MOVEMENT → SOUND → CUT / TRANSITION»

Example:

«0–5s: "<Subject 1>" stands on screen left, "<Subject 2>" stands on screen right. "<Subject 1>" faces "<Subject 2>", maintains eye contact, furrows his brows and speaks angrily. "<Subject 2>" listens silently and looks toward "<Subject 1>". Medium two-shot, camera positioned at a natural three-quarter angle, subtle slow push-in during the line. Natural room ambience, no background music.

5–5.5s: "<Subject 1>" finishes speaking. Both characters hold their positions naturally for a brief reaction beat. The camera settles naturally.

5.5s onward: Cut to a wider environmental shot only after the dialogue has finished.»

This is a planning structure, not a requirement to expose headings in the final H3 prompt unless the official H3 format requires them.

---

62. Natural Cinematic Editing Principle

Use editing to communicate information.

A cut should answer at least one of these:

- What should the viewer look at now?
- Whose reaction matters now?
- What new information is being revealed?
- Has the action changed?
- Has the emotional emphasis changed?
- Does the environment now matter?

If a cut has no useful purpose, prefer maintaining the current shot.

---

63. Character Performance Principle

Every principal character should feel alive.

When appropriate, combine:

«gaze + facial expression + posture + gesture + timing + dialogue»

Example:

«He briefly lowers his eyes, then looks back at her, raises one eyebrow, and gives a faint, sly smile before speaking.»

Do not turn every character into an exaggerated actor.

The target is:

«natural, expressive, believable performance.»

---

64. When Uncertain

When uncertain:

- whether a character should speak → KEEP SILENT
- whether another character is necessary → DO NOT ADD
- whether an object is necessary → DO NOT ADD
- whether to change the camera → KEEP THE CAMERA STABLE
- whether to cut → DO NOT CUT
- whether to describe appearance already established by reference → DO NOT REPEAT
- whether to invent dialogue → DO NOT INVENT
- whether to add background music → DO NOT ADD MUSIC

Preserve the user's explicit intent over cinematic improvisation.

---

65. Final Compilation Questions

Before producing the final prompt, silently answer:

1. Who are the characters?
2. How many physical characters are visible?
3. Where is each character?
4. What direction is each character facing?
5. Who is closer to camera?
6. Who is speaking?
7. Who is listening?
8. Where are their eyes looking?
9. What emotion is visible?
10. What exactly is each character doing?
11. What is the primary action?
12. What is the camera position?
13. What direction is the camera facing?
14. What shot size is being used?
15. Why does the camera move?
16. Why does the shot cut?
17. Has the important dialogue finished before a scenic cut?
18. Are relative character positions preserved?
19. Are reference-defined appearances being unnecessarily repeated?
20. Are subtitles accidentally requested?
21. Is any unrequested speech present?
22. Is background music accidentally present?
23. Is there natural transition time?
24. Does the entire sequence fit the requested duration?
25. Are Chinese and English versions semantically identical?

If any answer conflicts with the user's request, revise the prompt before output.

---

66. Core Principle

The H3 prompt should behave like a precise director's shooting plan, not a literary description.

The Skill must control:

«WHO → WHERE → FACING WHERE → DOING WHAT → FEELING WHAT → SAYING WHAT → LOOKING AT WHOM → CAMERA WHERE → CAMERA FACING WHERE → SHOT SIZE → CAMERA MOVEMENT → WHEN TO CUT → WHAT SOUND → HOW THE SHOT CONNECTS TO THE NEXT SHOT»

The most important principles are:

«Reference images define appearance; do not redundantly rewrite them.»

«Character positions and relative relationships remain locked unless the script explicitly changes them.»

«Characters speak only when authorized.»

«Characters who are not speaking remain silent and naturally expressive.»

«During dialogue, principal characters naturally look toward the person they are addressing.»

«Emotion must be expressed through observable facial and body behavior, not merely adjectives.»

«Camera movement and cuts should follow director logic and serve the story.»

«Important dialogue should normally finish before cutting to scenery.»

«No background music unless explicitly requested.»

«Each logical segment should retain approximately 0.5 seconds of natural visual continuity when timing allows.»

«When uncertain whether a character should speak, KEEP THE CHARACTER SILENT.»

«When uncertain whether an additional entity is necessary, DO NOT INTRODUCE IT.»

«When uncertain whether a camera movement or cut is necessary, KEEP THE SHOT STABLE.»

The final objective is not maximum cinematic complexity.

The final objective is:

«High prompt adherence + stable characters + stable spatial relationships + natural acting + controlled dialogue + coherent camera language + clean editing + temporal continuity.»