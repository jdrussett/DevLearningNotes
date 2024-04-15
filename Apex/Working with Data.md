# Working With Data

## General

---

- `.add()` method adds elements to a collection after it's been created
  - Example:

        List<String> colors = new List<String> {'red', 'green'};
        colors.add('blue');

  - Can add index parameter to `.add()` method (integer, placed before item to add to collection) to specify specific index you'd like the list item to have
  - Example:

        listOfFruits.add(4, 'pomegranate')

- `.addAll()` method adds all elements of one list *or set* to another list
- Can get collection elements with bracket notation (``list_variable[`desired_index`]``) or with `.get()` method

    > Indexing begins at 0 in Apex
    >
    >> Example: if variable `colors` is defined as `List<String> colors = new List<String> {'red', 'green', 'blue'}`, then `colors[1]` and `colors.get(1)` will both return `'green'`

---
---
> If you are working with maps, and you have a data type for the key set that *can change*, such as an sObject record that might acquire an ID after you insert it, you need to create a **clone** of the map after the final adjustments to the data, specifically the keys, have been made, otherwise you will not be able to find an exact match for the key if a field like ID has been added
---
---

- `.size()` method returns the size of a collection or the character count of a string, etc.
- `.put()` method on a map takes parameters for key and value; adds entries to a map
- `.get()` method returns value for a key provided on a map
  - If provided key is not mapped to a value, `get()` method returns null
- ``Date.newInstance(`yyyy`, `mm`, `dd`)`` function will define a date data point in Apex
- `Integer.valueOf()` returns the integer value of another data type like a string or a generic object
- Here is an example of looping through data locally with a map and performing dynamic value replacement with a map:

        List<LLC_BI__Entity_Compliance__c> ecList = [
            select id, name, LLC_BI__Age__c, LLC_BI__Entity__c, LLC_BI__HMDA_Applicant_Type__c, LLC_BI__HMDA_Credit_Score__c,
                LLC_BI__HMDA_Credit_Scoring_Model__c, LLC_BI__HMDA_Credit_Scoring_Model_Other__c,
                LLC_BI__HMDA_Ethnicity_Collection_Method__c, LLC_BI__HMDA_Ethnicity_Other__c, LLC_BI__HMDA_Ethnicity__c,
                LLC_BI__HMDA_Income__c, LLC_BI__HMDA_Not_Provided__c, LLC_BI__HMDA_Race_Collected__c,
                LLC_BI__HMDA_Race_Desc_Code_1__c, LLC_BI__HMDA_Race_Desc_Code_27__c, LLC_BI__HMDA_Race_Desc_Code_44__c,
                LLC_BI__HMDA_Race__c, LLC_BI__HMDA_Sex_Collection_Method__c, LLC_BI__HMDA_Sex__c,
                LLC_BI__Age_on_Application_Date__c,
                LLC_BI__Birthdate__c, LLC_BI__HMDA_Application_Date__c, LLC_BI__Is_Ethnicity_Collected_Visually__c,
                LLC_BI__Is_Manually_Edited__c, LLC_BI__Is_Race_Collected_Visually__c, LLC_BI__Is_Sex_Collected_Visually__c
            from LLC_BI__Entity_Compliance__c
        ];
        System.debug(ecList.size());
        Map<String, String> MyMap = new Map<String, String>{
            'Collected on the basis of visual observation or surname' => '1',
            'Not collected on the basis of visual observation or surname' => '2',
            'Not applicable' => '3',
            'No co-applicant' => '4'
        };
        for (LLC_BI__Entity_Compliance__c ec : ecList) {
            if (MyMap.containsKey(ec.LLC_BI__HMDA_Ethnicity_Collection_Method__c)) {
                ec.LLC_BI__HMDA_Ethnicity_Collection_Method__c = MyMap.get(ec.LLC_BI__HMDA_Ethnicity_Collection_Method__c);
            }
        }
        update ecList;

## Advanced Tips & Tricks

- __"Lazy-loading"__ a property in Apex (example):

      private static `data_type` `property_name` {
        get {
          if (property_name == null) {
            // do some stuff to populate it; SOQL query, call another method, etc.
          }
          return property_name;
        }
        set;
      }
