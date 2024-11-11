Disease Diagnosis Reasoner Package - DiagKnows

The disease diagnosis reasoner package is a set of knowledge representations and associated reasoning rules for use with the FIRE reasoner and NextKB package in Companions. Our goal with this package is to
create additional representation which can be used to assist with medical diagnosis and recommended tests for further information based on a patient's set of symptoms, and ranking the possible diagnoses
for a patient based on how frequently they occur in real-world patients. We hope this tool can be further developed into a strong aid for doctors and other medical professionals and increase the possibility of them
giving correct diagnoses.

Included Files:
ontology.krf - Contains all knowledge representations, added under the DiseaseDiagnosisMt Microtheory
inference_rules.krf - Contains our horn-clause reasoning, which defines how each possible query works
tests.krf - Contains test cases for our reasoning rules in the DiseaseDiagnosisTestMt Microtheory
DiagKnowsProjectReport.pdf - Contains our project writeup, including a more in depth description of our reasoner and knowledge, identified strengths and weaknesses of our representations, and possible next steps



How to use:

Load both the ontology.krf and inference_rules.krf files into the interaction manager in Companions. Then, browse the KB and go to the query tab, and set the Context to DiseaseDiagnosisMt.

To add a patient, enter the fact (isa ?PATIENTNAME Patient), replacing ?PATIENTNAME with the name of the patient and click "Tell".

To add symptoms that a patient has, enter the fact (patientHasSymptom ?PATIENTNAME ?SYMPTOM), replacing ?PATIENTNAME with the name of the patient and ?SYMPTOM with the symptom, then click "Tell".

To see all the possible diagnoses for a patient, enter the query (possibleDiagnosis ?PATIENTNAME ?disease), replacing ?PATIENTNAME with the name of the patient and click "Query using fire:query".

To see the recommended tests for a patient, enter the query (recommendedTest ?PATIENTNAME ?test), replacing ?PATIENTNAME with the name of the patient and click "Query using fire:query".

To see the list of a the possible diagnoses for a patient ordered from most common to least common, enter the query (evaluate ?s (SortFn (TheClosedRetrievalSetOf ?d (possibleDiagnosis ?PATIENTNAME ?d)) lessThan (FunctionToArg 2 diseaseHasFrequency))), 
replacing ?PATIENTNAME with the name of the patient and click "Query using fire:query".

To use the test cases with predifined patients and their corresponding symptoms, set the Context to DiseaseDiagnosisTestMt and run any of the commented out queries in the tests.krf file.



How to build up on the knowledge base:

To add symptoms:
genls the new symptom to the Symptom collection.
example:  (genls Blindness Symptom)

To add diseases: 
genls the new disease to the DiseaseType collection
example: (genls Migraine DiseaseType)

To map a symptom to a disease:
use the binary predicate diseaseHasSymptomType with disease as the first argument and symptom as the second argument.
example: (diseaseHasSymptomType Migraine Blindness)

To create a test:
genls the new test to MedicalTesting collection.
example: (genls UltraSound MedicalTesting)

To map a test to a disease:
use the binary predicate medicalTestRelevantToPhysiologicalConditionType with test as first argument and disease as the second argument.
example: (medicalTestRelevantToPhysiologicalConditionType UltraSound Synovitis)

Add frequency of occurence to a disease:
use the binary predicate diseaseHasFrequency with disease as the first argument and frwquency number as the second argument.
example: (diseaseHasFrequency Migraine 2)
