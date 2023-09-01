## NLU engine
Main intent is request_doctor appointment. The workflow to ask questions will be triggered only when the intent is successful

Basic information captured by (Rasa) NLU engine are
- Name
- DOB
- Reason for calling/ (medical complaint)
- contact number

Rasa NlU is trained on the above entities and will extract entities from text. Using Rasa Forms to capture the all the information to fill all the required slots of informations. The worflow is triggered once doctor appointment booking intent is identified.

## Extension
We capture only limited information from the patient in the form but it can easily be extended to more entities.
- Collect insurance information
    - Payer name and ID
- Ask if they have a referral, and to who

## Train

pipeline:
- name: WhitespaceTokenizer
- name: RegexFeaturizer
- name: LexicalSyntacticFeaturizer
- name: CountVectorsFeaturizer
- name: DIETClassifier
- name: FallbackClassifier

Using whitespace to tokenize the text, regex featurizer identifies pattern in the text (good for  features with a pattern contact number and date of birth), lexical featurizer identifies syntax in the text. DIET is dual intent and entity transformer, helps with both intent and entity extraction.
Fallback classfier is used for identifying and handling unknownintent and helps with model with gracefully handling the rules workflow.


To train the model simply run
```
rasa train
```

## Test
To see the performance of the DIET classifier run. It would generate the confusion matrix and errors from the classfier.
```
rasa test 
```

## Hosting

```
nlu_engine % rasa run -m models --enable-api --endpoints endpoints.yml --cors "*"
```