RegisterResourceGenerationFunction("IOTMPeaceTurkeyGenerateResource");
void IOTMPeaceTurkeyGenerateResource(ChecklistEntry [int] resource_entries)
{
	if (!lookupFamiliar("Peace Turkey").familiar_is_usable()) return;

	// Purkey Title
//still needs a fix for famwt when not active (currently returns 0 but still functions)
    int turkeyProc = 24;
	if (my_familiar() == lookupFamiliar("peace turkey"));
	{
		int turkeyProc = 24 + sqrt(effective_familiar_weight($familiar[peace turkey]) + weight_adjustment());	
	}
	int PeasCount = available_amount($item[whirled peas]);
	int PeaSoupCount = available_amount($item[handful of split pea soup]);
	string [int] description;
	string url = "familiar.php";
	{
		description.listAppend("" + PeasCount + " peas available (need to paste them)");
		description.listAppend("" + PeaSoupCount + " peabanishers available");
		resource_entries.listAppend(ChecklistEntryMake("__familiar peace turkey", url, ChecklistSubentryMake(HTMLGenerateSpanFont(turkeyProc +"% Peace Turkey proc", "black"), "", description), 2));
	}
	if ($item[handful of split pea soup].available_amount() > 0 )
    {
        resource_entries.listAppend(ChecklistEntryMake("__item handful of split pea soup", "", ChecklistSubentryMake(pluralise($item[handful of split pea soup]), "", "Free run/banish. Also have " + PeasCount + " peas."), 0).ChecklistEntrySetCombinationTag("banish").ChecklistEntrySetIDTag("Purkey banish"));
    }
}
