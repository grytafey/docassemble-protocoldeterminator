The Protocol Determinator makes it easier for advocates to use data to determine a person's legal needs, and refer to available protocols or otherwise provide specific legal information.

Civil common law as best, most elegant solution.

Our system is failing 

Open types of organization, with open tools for as many people as possible to participate, can provide the open, uniform law.

The Protocol Determinator demonstrates both how we can = provide the best assistance we can to people who need help now while building a better system in the future.

## Gathering Data from Pika and Elsewhere

The Protocol Determinator can be opened in Pika, and pull data from any of the tabs.  The data that is pulled from Pika can be double-checked.

<details>
	<summary>Software issues</summary>
	
###### Software issues
	1. Get data from related parties to the case
	   * link to issues
	2. Add in explanation about 1 and 0 as True and False
	   * link to issues
</details>

<details>
	<summary>Features Requests</summary>
	
###### Features Requests
	1. Pull in data from other sources
	   2. Court dockets
	   3. Property lists
	1. Add tab for protocol determinator
	   
</details>

<details>
	<summary>How it works in docassemble</summary>
	
<br>	
docassemble uses a javascript function to put data from Pika into the fields of a docassemble interview.  Hitting the button at the bottom of the screen brings the data into the docassemble interview.

    ---
    question: Pika Field import
    fields:
      - Address: address
        required: false
      - Case Zip Code: case_zip_code
        required: false
      - Case County: countyAC
        required: false
      - Date Intake Completed: date_intake_completed
        required: false
        datatype: date
      - Hearing Date: hearing_date
        required: false
      - Client Age: client_age
        required: false
        datatype: integer
      - Domestic Violence: domestic_violence
        required: false
      - Sexual Assault: sexual_assault
        required: false
      - Stalking: stalking
        required: false
      - Opposing Party: opposing_party
        required: false
      - Calculated Poverty Rate from Assets Screen: calc_poverty
        required: false
        datatype: number
      - Adjusted Poverty Rate from Liabilities Screen: adj_poverty
        required: false
        datatype: number
      - Minor Children: minor_children
        required: false
        datatype: integer
      - Is applicant receiving any public benefits?: public_benefits
        required: false
      - Problem Code: problem_code
        required: false
      - Special Problem Code: special_problem_code
        required: false
      - Case Number: number
        required: false
    continue button field: pikagathered
    script: |
      <script>
      // address
      document.getElementById('YWRkcmVzcw').value = pika_js["client_address"];
      // Client age
      document.getElementById('Y2xpZW50X2FnZQ').value = pika_js["client_age"];
      // Hearing Date
      document.getElementById('aGVhcmluZ19kYXRl').value = pika_js["date_hearing"];
      // Number
      document.getElementById('bnVtYmVy').value = pika_js["number"];
      // Case County
      document.getElementById('Y291bnR5QUM').value = pika_js["county"];
      // Domestic Violence
      document.getElementById('ZG9tZXN0aWNfdmlvbGVuY2U').value = pika_js["dom_abuse"];
      // Sexual Assault
      document.getElementById('c2V4dWFsX2Fzc2F1bHQ').value = pika_js["sex_assault"];
      // Stalking
      document.getElementById('c3RhbGtpbmc').value = pika_js["stalking"];
      // Date Intake Completed
      document.getElementById('ZGF0ZV9pbnRha2VfY29tcGxldGVk').value = pika_js["completed_date"];
      // Case Zip Code
      document.getElementById('Y2FzZV96aXBfY29kZQ').value = pika_js["case_zip"];
      // Calculated Poverty Rate from Assets Screen
      document.getElementById('Y2FsY19wb3ZlcnR5').value = pika_js["poverty"];
      // Adjusted Poverty Rate from Liabilities Screen
      document.getElementById('YWRqX3BvdmVydHk').value = pika_js["recalc_poverty"];
      // Minor Children
      document.getElementById('bWlub3JfY2hpbGRyZW4').value = pika_js["children"];
      // Is applicant receiving any public benefits?
      document.getElementById('cHVibGljX2JlbmVmaXRz').value = pika_js["public_benefits_recipient"];
      // Problem Code
      document.getElementById('cHJvYmxlbV9jb2Rl').value = pika_js["problem"];
      // Special Problem Code
      document.getElementById('c3BlY2lhbF9wcm9ibGVtX2NvZGU').value = pika_js["sp_problem"];
      
      //this section un-squishes the docassemble interview when embedded in a Pika tab
      // div with dabody class - remove col, add container-fluid
      $(".dabody").removeClass("col");
      $(".dabody").addClass("container-fluid");

      // class span8, replace with container-fluid
      $(".span8").addClass("container-fluid");
      $(".span8").removeClass("span8");

      // id page_content, change container to container-fluid
      $('#page_content').addClass("container-fluid");
      $('#page_content').removeClass("container");
       </script>

    ---

</details>

<details>
	<summary>Connected Airtable databases</summary>
	
<br>	
This section is not directly connected to Airtable, but the Pika variables collected here are listed in the [facts table of the Legal Objects Library](https://airtable.com/shromaQ1J1QXNO5n2).	
    
    
</details>

## Selecting Specific Issues and Clones

The interview allows you to pick the specific legal issue by selecting subsets within an issue and a "clone" issue when appropriate.  A clone issue is the same issue that has different information because of the different jurisdiction or the stage of the problem.

<details>
	<summary>Software issues</summary>
	
###### Software issues
	1. Get data from related parties to the case
	   * link to issues
	2. Add in explanation about 1 and 0 as True and False
	   * link to issues
</details>

<details>
	<summary>Features Requests</summary>
	
###### Features Requests
	1. Pull in data from other sources
	   2. Court dockets
	   3. Property lists
	   
</details>

<details>
	<summary>How it works in docassemble</summary>
	
<br>	
The interview needs to complete apps.issues, a list of

The first issue - the "Top" issue - is added automatically.  This is the issue object for all types of legal objects, with subsets like "Housing", "Family".  We can add the 'Top' issue by using the issue2aid dictionary in the LegalObjectsLibrary_dictionary.yml.

	---
	code: |
	  app.issues.there_are_any = True
	---
	code: |
	  app.issues[0].a_id = issues2aid['Top']
	---

</details>

<details>
	<summary>Connected Airtable databases</summary>
	
<br>	
Issue Objects are in the LegalObjectLibrary base in the issues tab. [Here is a viewy]().	
    
    
</details>


## Finding Legal Defenses

If an IssueObject involves or could involve some legal procedure like a court case, the protocol determinator will ask questions about the case using LegalObjects.

LegalObjects are similar to IssueObjects, but instead of having subsets to narrow down to a specific issue, LegalObjects have elements, like a court case has elements.  These are parts of a court case that must be proven to be successful in court.

Organizing law into elements is natural to lawyers, and also translates well to organiing information into objects for docassemble.  The protocol determinator can go down the relevant paths of the elements to find any potential defenses.

The necessary key to succes creating progammatic law is to make an interface that looks like the law to lawyers, who are going to be creating the contaent.  Adding an element or defense is much simpler thean reconfiguring a low chart or branching logic tree.

<details>
	<summary>Software issues</summary>
	
###### Software issues
	1. Get data from related parties to the case
	   * link to issues
	2. Add in explanation about 1 and 0 as True and False
	   * link to issues
</details>

<details>
	<summary>Features Requests</summary>
	
###### Features Requests
	1. Pull in data from other sources
	   2. Court dockets
	   3. Property lists
	   
</details>

<details>
	<summary>How it works in docassemble</summary>
	
<br>	
The app.legal_objects DAList is first populated by any Legal Objects associated with an IssueObject that was selected.

	code: |
	  for issue in app.issues:
		if hasattr(issue,'legalObjects'):
		  for legOb in issue.legalObjects:
		    app.legal_objects.append(legob_from_a_id(legOb))
	  app.legal_objects.gathered = True
	comment: |
	  Adds LegalObjects to issues
	---

	---
	generic object: LegalObject
	sets: x.legal_elements
	code: |
	  x.initializeAttribute('legal_elements',LegalObjectList.using(object_type=LegalObject, auto_gather = False))
	  for atid in x.elementslist:
		tempobject = legob_from_a_id(atid)
		if tempobject.active:
		  x.legal_elements.append(tempobject,set_instance_name=True)
	  x.legal_elements.gathered = True
	comment: |
	  Adds LegalObjects to LegalObjects.  This is where I need to add something to screen out some LegalObjects.  LegalObjects can have a condition and only be added if that condition is true.  So for Corporate Plaintiff would have as a factObject whether the Plaintiff was a fictitious name.  Each of the elements of Corporate Plaintiff should only be added as a legal element if the Plaintiff is a fictitious name.  The Grounds legalObject has a factObject what the stated grounds in the complaint.  Each of the elements can have a condition that only adds the elements for their case - the Nonpayment LegalObject will have a condition [grounds_in_the_complaint="Nonpayment"]
	  So do I need an exec command here
	---
	code: |
	  if not defined('used_defenses'):
		used_defenses = list()
	---
	generic object: LegalObject
	code: |
	  if x.more_clones == "No_More_Clones":
		if not hasattr(x, 'factslist'):
		  if x.legal_elements.ismet:
		    x.ismet = True
		  else:
		    x.ismet = False
		else:
		  if x.facts_elements_interaction == "factsANDelements":
		    if not x.facts.ismet:
		      x.ismet = x.facts.ismet
		    else:
		      if x.legal_elements.ismet:
		        x.ismet = True
		      else:
		        x.ismet = False
		  elif x.facts_elements_interaction == "factsORelements":
		    if x.facts.ismet:
		      x.ismet = True
		    else:
		      if x.legal_elements.ismet:
		        x.ismet = True
		      else:
		        x.ismet = False
		  else:
		    x.ismet = x.facts.ismet
	  else:
		reconsider('x.more_clones')
	  if defined('x.defensename') and x.ismet is not None:
		setattr(app.case,x.defensename,x.ismet)
		used_defenses.append(x.defensename)
	comment: |
	  The interview determines whether LegalObjects are "met", meaning that the LegalObject is True if it helps the Plaintiff win the type of case associated with the top-level LegalObject.
	  First, it is checked whether there are any clones of the LegalObject.  A clone is the same legal issue with different rules because of a different jurisdiction or type of housing.
	  Next, it checks whether "facts", which is a list of FactObjects, is "met".  It checks this by prompting a FactObject question, and then using the response in a formula, as described in that block.
	  Facts are checked first for two reasons.  First, if a LegalObject has both FactObjects and other LegalObjects as elements, it means that each of the element LegalObjects require that FactObject to be a certain answer.  For example, the Corporate Plaintiff has a FactObject about whether the Plaintiff is a corporation.  If the Plaintiff is not a corporation, then the "facts" is met, and the LegalObjects shouldn't be checked.  Right now, it doesn't work this way - if the facts.ismet = False, then the legalObject is false, and it won't need to ask the other questions.  (What about the situation where a fact object might be cuz of a defense (defense that there is no notice) but if there is notice, then these other defenses should be checked.
	  Second, LegalObjects that are elements of a LegalObject with a FactObject may be conditioned on how that FactObject question is answered.  For example, Grounds has a FactObject of grounds_listed_in_complaint.  After asking what grounds are listed in the complaint, the LegalObjects are only relevant if the grounds listed.  So if the grounds is "Nonpayment", only the Nonpayment LegalObject will be relevant, and the Rule Violations are nto relevant (meaning they can be marked .ismet - .ismet includes not being relevant.)
	  So I have to make it so that if in Corporate Plaintiff, is_fictitious_name = False evaluates to True, and the legal objects are not needed and the legal object is not added to defense.  If is_fictitious_name = True, the fact formula evaluates to False and the legal objects are not needed.
	  In the case of Grounds, the fact_formula should always evaluate to False, so the legalObjects are always evaluated
	  In a "final" LegalObject, where there are no elements, then if there is a defense, facts.ismet should be False, and then the legalobject would be False.
	---
	generic object: LegalObjectList
	code: |
	  counter = 0
	  for legalobject in x:
		if legalobject.ismet or legalobject.ismet is None:
		  counter += 1
	  if counter == len(x):
		x.ismet = True
	  else:
		x.ismet = False
	comment: |
	  This section determines if an legal object is "met" by seeing if each of the legal objects in the elements fields are met.  
	---
	generic object: LegalObject
	sets: 
	  - x.facts
	code: |
	  if hasattr(x,'factslist'):
		x.facts.there_are_any = True
		for fid in x.factslist:
		  x.facts.append(fact_from_a_id(fid),set_instance_name=True)
		  if hasattr(x,'explanationifnotmet'):
		    x.facts.explanationifnotmet = x.explanationifnotmet
		x.facts.there_is_another = False
	  else:
		x.facts.there_are_any = False
	comment: |
	  This section adds fact objects to a legal object from the AirTable.  I think I need to add in something to screen for active fact objects.
	---
	generic object: FactObjectList
	code: |
	  x.factsgathered
	  exec(x.fact_formula)
	  x.ismet = facts_are_met()
	comment: |
	  The formula in the AirTable is called, which looks for the definition of the variables in the formula.  Is it even necessary to have the facts as children.  A sample fact_formula looks like this
	  def facts_are_met():
		if notice_exists and notice_attached_to_complaint:
		  return True
		else:
		  return False
	  So are the variables in the fact_formula set, in this case "notice_exists" and "notice_attached_to_complaint".  If that is the case, then I can put things like that in the fact_formula and still just evaluate to True/False.  But what does True or False mean for something like Corporate_Plaintiff?  The LegalObject should be True if the Plaintiff is either not a corporation or if all the legal objects are met.  So the fact_formula should evaluate to True if the Plaintiff is not a corporation, and to False if
	---
	generic object: FactObjectList
	sets: x[0]
	question:  ${ x.label }
	subquestion: |
	  ${ x.explanation }
	  
	  ${ x.question }

	  % if hasattr(x,'html'):
	  ${ x.html }
	  % endif

	  
	fields:
	  code: x.questioncode()
	continue button field: x.factsgathered
	comment: |
	  The question for facts - the explanation are set by tables in the AirTable 

	---
	generic object: FactObjectList
	code: |
	  if defined('finish_questions'):
		x.factsgathered = True
	---
	code: |
	  app.match_dict.new(protocols.keys())
	  for protokey in protocols.keys():
		app.match_dict[protokey].qualify_sentence = protocols[protokey].qualify_sentence
		for sfkey in protocols[protokey].keys():
		  if not set(protocols[protokey][sfkey]).isdisjoint(set(app.specific_factors[sfkey])):
		    app.match_dict[protokey][sfkey] = True
		  else:
		    app.match_dict[protokey][sfkey] = False
		    app.match_dict[protokey].gathered = True
		    break
		app.match_dict[protokey].gathered = True
	  app.match_dict.gathered = True
	comment: |
	  This section determines if each requirement in the protocol is satisfied by seeing if there is any overlap between the protocol's set of airtable ids in protocols['HCED1a']['County'] with the set of AirTable ids from the same table in specific_factors['County'].  If there is an overlap (or not disjoint), then it will set match_dict['HCED1a']['County'] to True.  A block below with then see if the all of the factors in match_dict['HCED1a'] are true.
	---
	generic object: Protocol
	code: |
	  exec(x.qualify_sentence)
	  x.qualify = qualify()
	comment: |
	  This section runs the qualify_sentence from the Protocols table, which will look something like this:
	  
	  def qualify():
		if date_of_hearing > date_intake_completed.plus(days=3):
		  if domestic_violence or sexual_assault or stalking:
		    return 1
		  elif disability_household_member:
		    return 1
		  else:
		    return 0
		else:
		  return 0
		
	  The formula statement uses FactObject variable names and causes the interview to ask questions to define those variables.  Why does this one use "Good" or "Bad"?  That's obviously a mistake.  The next block tests to see if it is equal to 1.  So this protocol will never "qualify".
	---
	generic object: LegalObject
	code: |
	  if hasattr(x,'clones') and len(x.clones) > 0:
		x.clone_from_a_id(x.clone_legob, x.clone_name)
		if hasattr(x,'clones') and len(x.clones) > 0:
		  x.more_clones = "May_Be_More_Clones"
		else:
		  x.more_clones = "No_More_Clones"
	  else:
		x.more_clones = "No_More_Clones"
	comment: |
	  Checks to see if there are clones.  If there are, a LegalObject method is used to update the current LegalObject, by replacing any of the information fields when that information field is not blank in the clone object.
	  Because the object is updated, it can check clones again.  The clones field will always change, because the clone will not appear in the clones field.  So it checks to see if there are clones.  x.more_clones is called in the .ismet evaluation block, and if x.more_clones is not equal to "No_More_Clones", then x.more_clones gets reconsidered, forcing it to come back to this block.

	---
	generic object: LegalObject
	sets: x.clone_legob
	code: |
	  for key, value in x.clones.iteritems():
		x.clone_name = key
		clone_temp_list = list()
		for clone_lo_id in value:
		  clone_type_id = get_clone_type(clone_lo_id,key)
		  if clone_type_id in app.specific_factors[key]:
		    x.clone_legob = clone_lo_id
	comment: |
	  This sets a variable need for clone_from_a_id.  x.clone_legob is the Airtable id for the clone legal object.  The clones attribute of legal object is a set of Airtable ids of clones, which are also in the legal objects table.  However, to pick which clone is appropriate, the user will pick the name of the clone.  The clone legal object will be something like "Notice Public Housing", but the user should pick from a list with labels like "Public Housing".  In addition, the user may have already set "Public Housing" as a specific factor, but that will be set as a specific factor, and not as the name of that clone.  So this table checks each of the 
	  This just picks the last clone in x.clones.

	---
</details>

<details>
	<summary>Connected Airtable databases</summary>
	
<br>	
Issue Objects have a field legalObjects, which is a list of Airtable ids of rows in the legalobjects tab.

Legal Objects are in the LegalObjectLibrary base in the legalobjects tab. [Here is a viewy]().	
    
    
</details>


## Matching Protocols

After figuring out the IssueObject and the LegalObject, the Protocol determinator can sometimes determine if a protocol is met and a client can be referred.  Or more questions may need tob e asked.  The protocol determinator will ask needed questions and then determine the protocol.

A protocol can be created by selecting counties, issue objects and legal objects form a list.  If a protocol only applies to certain populations those questions are added as FactObjects, also used by LegalObjects.  These FactObjects are used in a formula in the Airtable to see if a protocol is met.  Using this method balances the ease of creating protocols with the flexibility needed to allow for different kinds of protocols.

<details>
	<summary>Software issues</summary>
	
###### Software issues
1. Opposing_Parties are asked even if there is no matching zip code.
	
</details>

<details>
	<summary>Features Requests</summary>
	
###### Features Requests
1. Make a docassemble interview to input protocols
2. Automatically make referral letter if protocol determined
1. Make no-code system to create formula in docassemble interview
	   
</details>

<details>
	<summary>How it works in docassemble</summary>
	
<br>	
Protocols are inputted at the beginning

	---
	code: |
	  app.issues.there_are_any = True
	---
	code: |
	  app.issues[0].a_id = issues2aid['Top']
	---

</details>

<details>
	<summary>Connected Airtable databases</summary>
	
<br>	
Protocols are in the LegalObjectLibrary base in the protocols tab. [Here is a viewy]().	
    
    
</details>



## Creating Information Sheets

The specific legal issue leads you to the specific legal information that is most helpful.

The infosheet is organized into 3 parts to give the user the "news they can use":

1. Explanations
1. Next Steps
1. Options



The first time a new issue, or a new clone of an existing issue, an advocate will be presented with legal information about the .  The advocate can organize this information that is most understandable, 

### Gathering

### Next Steps and Options

Next steps and options are collected from the layers of issues and legal objects.  For example, an option in all eviction cases would be Request a Continuance, but File Counterclaims may only be relevant for certain elements of an eviction case.


<details>
	<summary>Software issues</summary>
	
###### Software issues
	1. Get data from related parties to the case
	   * link to issues
	2. Add in explanation about 1 and 0 as True and False
	   * link to issues
</details>

<details>
	<summary>Features Requests</summary>
	
###### Features Requests
	1. Send notification to advocate when there is an issue that isn't completed
	   
</details>

<details>
	<summary>How it works in docassemble</summary>
	
<br>	
The interview needs to complete apps.issues, a list of

The first issue - the "Top" issue - is added automatically.  This is the issue object for all types of legal objects, with subsets like "Housing", "Family".  We can add the 'Top' issue by using the issue2aid dictionary in the LegalObjectsLibrary_dictionary.yml.

	---
	code: |
	  app.issues.there_are_any = True
	---
	code: |
	  app.issues[0].a_id = issues2aid['Top']
	---

</details>

<details>
	<summary>Connected Airtable databases</summary>
	
<br>	
Issue Objects are in the LegalObjectLibrary base in the issues tab. [Here is a viewy]().	
    
    
</details>
