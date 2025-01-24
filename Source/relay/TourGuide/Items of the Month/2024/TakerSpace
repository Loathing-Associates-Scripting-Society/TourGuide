//Takerspace
RegisterResourceGenerationFunction("IOTMTakerspaceGenerateResource");
void IOTMTakerspaceGenerateResource(ChecklistEntry [int] resource_entries)
{
	//you wouldn't download a boat
	if (__iotms_usable[lookupItem("TakerSpace letter of Marque")]) return;
	
	string [int] description;
	string url = "campground.php?action=workshed";
	int TSAnchors = get_property_int("takerSpaceAnchor");
	int TSGold = get_property_int("takerSpaceGold");
	int TSMasts = get_property_int("takerSpaceMast");
	int TSRum = get_property_int("takerSpaceRum");
	int TSSilk = get_property_int("takerSpaceSilk");
	int TSSpice = get_property_int("takerSpaceSpice");
	
	if (TSAnchors + TSGold + TSMasts + TSRum + TSSilk + TSSpice > 0) 
	{
		description.listAppend(HTMLGenerateSpanOfClass("Spices: ", "r_bold") + "" + TSSpice + "");
		description.listAppend(HTMLGenerateSpanOfClass("Rum: ", "r_bold") + "" + TSRum + "");
		description.listAppend(HTMLGenerateSpanOfClass("Anchors: ", "r_bold") + "" + TSAnchors + "");
		description.listAppend(HTMLGenerateSpanOfClass("Masts: ", "r_bold") + "" + TSMasts + "");
		description.listAppend(HTMLGenerateSpanOfClass("Silk: ", "r_bold") + "" + TSSilk + "");
		description.listAppend(HTMLGenerateSpanOfClass("Gold: ", "r_bold") + "" + TSGold + "");
		
		if ($item[pirate dinghy].available_amount() == 0 ) {
			description.listAppend(HTMLGenerateSpanFont("Boat: 1 anchor/1 mast/1 silk", "blue"));
		}
		if ($item[deft pirate hook].available_amount() == 0 ) {
			description.listAppend(HTMLGenerateSpanFont("Hook: 1 anchor/1 mast/1 gold", "blue"));
		}
		if ($item[jolly roger flag].available_amount() == 0 ) {
			description.listAppend(HTMLGenerateSpanFont("Flag: 1 rum/1 mast/1 silk/1 gold", "blue"));
		}
		resource_entries.listAppend(ChecklistEntryMake("__item pirate dinghy", url, ChecklistSubentryMake("Takerspace resources", description), 1));
	}
}
