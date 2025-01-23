string [int] SSkillsPotentialCraftingOptions()
{
    string [int] potential_options;
    if ($item[knob cake].available_amount() == 0 && !__quest_state["Level 6"].finished && my_path().id != PATH_COMMUNITY_SERVICE)
        potential_options.listAppend("knob cake");
    if (__misc_state["can eat just about anything"])
        potential_options.listAppend("food");
    if (__misc_state["can drink just about anything"])
        potential_options.listAppend("drink");
    if ($skill[advanced saucecrafting].skill_is_usable())
        potential_options.listAppend("sauceror potions");
    return potential_options;
}

void SSkillsGenerateResource(ChecklistEntry [int] resource_entries)
{
    if (skill_is_usable($skill[inigo's incantation of inspiration])) {
        int inigos_casts_remaining = 5 - get_property_int("_inigosCasts");
        string description = SSkillsPotentialCraftingOptions().listJoinComponents(", ").capitaliseFirstLetter();
        if (inigos_casts_remaining > 0)
            resource_entries.listAppend(ChecklistEntryMake("__effect Inigo's Incantation of Inspiration", "skills.php", ChecklistSubentryMake(pluralise(inigos_casts_remaining, "Inigo's cast", "Inigo's casts") + " remaining", "", description), 4).ChecklistEntrySetIDTag("Inigo inspiration skill reminder"));
    }
    if (true) {
        ChecklistEntry craft_entry;
        craft_entry.image_lookup_name = "__item tenderizing hammer";
        craft_entry.url = "craft.php?mode=discoveries";
        craft_entry.tags.id = "Free crafts resource";
        craft_entry.importance_level = 4;

        int free_crafts_left = 0;
        int free_cooks_left = 0;
        int free_mixes_left = 0;
        if ($effect[Inigo's Incantation of Inspiration].have_effect() >= 5) {
            free_crafts_left += $effect[Inigo's Incantation of Inspiration].have_effect() / 5;
        }
        if ($effect[craft tea].have_effect() >= 5) {
            free_crafts_left += $effect[craft tea].have_effect() / 5;
        }
        if ($skill[rapid prototyping].skill_is_usable()) {
            free_crafts_left += clampi(5 - get_property_int("_rapidPrototypingUsed"), 0, 5);
        }
        if (lookupSkill("Expert Corner-Cutter").skill_is_usable()) {
            free_crafts_left += clampi(5 - get_property_int("_expertCornerCutterUsed"), 0, 5);
        }    
        if (get_property_int("homebodylCharges") > 0) {
            free_crafts_left += (get_property_int("homebodylCharges"));
        }
        // adding cookbookbat free crafts into crafting tile        
        if (lookupFamiliar("Cookbookbat").familiar_is_usable()) {
            string [int] description;
			free_cooks_left += clampi(5 - get_property_int("_cookbookbatCrafting"), 0, 5);
			string title = "free cooking";
			if (free_cooks_left > 0) {
			craft_entry.subentries.listAppend(ChecklistSubentryMake(pluralise(free_cooks_left, title, title + "s") + " remaining", free_crafts_left > 0 ? "COOKING only" : "", description));
			}
        }
		// holiday multitasking
		if (lookupSkill("Holiday Multitasking").skill_is_usable()) {
            free_crafts_left += clampi(3 - get_property_int("_holidayMultitaskingUsed"), 0, 3);
        }    
        // elf guard cooking
        if (lookupSkill("Elf Guard Cooking").skill_is_usable()) {
            string [int] description;
			free_cooks_left += clampi(3 - get_property_int("_elfGuardCookingUsed"), 0, 3);
			string title = "free cooking";
			if (free_cooks_left > 0) {
			craft_entry.subentries.listAppend(ChecklistSubentryMake(pluralise(free_cooks_left, title, title + "s") + " remaining", free_crafts_left > 0 ? "COOKING only" : "", description));
			}
        }
		// cocktails of the age of sail
        if (lookupSkill("Old-School Cocktailcrafting").skill_is_usable()) {
            string [int] description;
			free_mixes_left += clampi(3 - get_property_int("_oldSchoolCocktailCraftingUsed"), 0, 3);
			string title = "free mixing";
			if (free_mixes_left > 0) {
			craft_entry.subentries.listAppend(ChecklistSubentryMake(pluralise(free_mixes_left, title, title + "s") + " remaining", free_crafts_left > 0 ? "MIXING only" : "", description));
			}
        }

        int free_smiths_left = 0;
        if (__campground[$item[warbear auto-anvil]] > 0) {
            free_smiths_left += clampi(5 - get_property_int("_warbearAutoAnvilCrafting"), 0, 5);
        }
        int jackhammer_crafts_later = 0;
        if ($items[Loathing Legion abacus,Loathing Legion can opener,Loathing Legion chainsaw,Loathing Legion corkscrew,Loathing Legion defibrillator,Loathing Legion double prism,Loathing Legion electric knife,Loathing Legion flamethrower,Loathing Legion hammer,Loathing Legion helicopter,Loathing Legion jackhammer,Loathing Legion kitchen sink,Loathing Legion knife,Loathing Legion many-purpose hook,Loathing Legion moondial,Loathing Legion necktie,Loathing Legion pizza stone,Loathing Legion rollerblades,Loathing Legion tape measure,Loathing Legion tattoo needle,Loathing Legion universal screwdriver,Loathing Legion Knife].available_amount() > 0) {
            int jackhammer_crafts = clampi(3 - get_property_int("_legionJackhammerCrafting"), 0, 3);
            if ($item[Loathing Legion jackhammer].available_amount() == 0)
                jackhammer_crafts_later = jackhammer_crafts;
            else
                free_smiths_left += jackhammer_crafts;
        }
        if ($item[Thor's Pliers].available_amount() > 0) {
            free_smiths_left += clampi(10 - get_property_int("_thorsPliersCrafting"), 0, 10);
        }
        if (free_smiths_left > 0 || jackhammer_crafts_later > 0) {
            craft_entry.url = "craft.php?mode=discoveries&what=smith";
            //free_smiths_left += free_crafts_left; //naaaah
            //FIXME remind them to buy a hammer (if no loathing jackhammer)
            string [int] description;
            if (jackhammer_crafts_later > 0)
                description.listAppend("Get " + jackhammer_crafts_later + " more by folding your loathing legion knife into jackhammer.");
            string title = "free smithing";
            if (knoll_available()) //innabox makes normal smithing free
                title = "free advanced smithing";
            craft_entry.subentries.listAppend(ChecklistSubentryMake(pluralise(free_smiths_left, title, title + "s") + " remaining", free_crafts_left > 0 ? "SMITHING only" : "", description));
        }

        if (free_crafts_left > 0) {
            string description = SSkillsPotentialCraftingOptions().listJoinComponents(", ").capitaliseFirstLetter();
            craft_entry.subentries.listAppend(ChecklistSubentryMake(pluralise(free_crafts_left, "free craft", "free crafts") + " remaining", free_smiths_left > 0 || jackhammer_crafts_later > 0 ? "Any crafting mode, including smithing" : "", description));
        }

        if (craft_entry.subentries.count() > 0)
            resource_entries.listAppend(craft_entry);
    }

    ChecklistSubentry [int] subentries;
    int importance = 11;
    string url;

    string [skill] skills_to_details;
    string [skill] skills_to_urls;
    string [skill] skills_to_title_notes;
    skill [string][int] property_summons_to_skills;
    int [string] property_summon_limits;

    property_summon_limits["reagentSummons"] = 1;
    property_summon_limits["noodleSummons"] = 1;
    property_summon_limits["cocktailSummons"] = 1;
    property_summon_limits["grimoire1Summons"] = 1;
    property_summon_limits["grimoire2Summons"] = 1;
    property_summon_limits["grimoire3Summons"] = 1;
    property_summon_limits["_grimoireGeekySummons"] = 1;
    property_summon_limits["_grimoireConfiscatorSummons"] = 1;
    property_summon_limits["_candySummons"] = 1;

    if ($skill[advanced saucecrafting].have_skill() && $skill[advanced saucecrafting].skill_is_usable())
        property_summons_to_skills["reagentSummons"] = listMake($skill[advanced saucecrafting], $skill[the way of sauce]);
    if ($skill[Pastamastery].have_skill() && $skill[Pastamastery].skill_is_usable())
        property_summons_to_skills["noodleSummons"] = listMake($skill[Pastamastery], $skill[Transcendental Noodlecraft]);
    if ($skill[Advanced Cocktailcrafting].have_skill() && $skill[Advanced Cocktailcrafting].skill_is_usable())
        property_summons_to_skills["cocktailSummons"] = listMake($skill[Advanced Cocktailcrafting], $skill[Superhuman Cocktailcrafting]);
    property_summons_to_skills["_coldOne"] = listMake($skill[Grab a Cold One]);
    property_summons_to_skills["_spaghettiBreakfast"] = listMake($skill[spaghetti breakfast]);
    property_summons_to_skills["_discoKnife"] = listMake($skill[that's not a knife]);
    property_summons_to_skills["_lunchBreak"] = listMake($skill[lunch break]);
    property_summons_to_skills["_psychokineticHugUsed"] = listMake($skill[Psychokinetic Hug]);
    property_summons_to_skills["_pirateBellowUsed"] = listMake($skill[Pirate Bellow]);
    property_summons_to_skills["_holidayFunUsed"] = listMake($skill[Summon Holiday Fun!]);
    property_summons_to_skills["_summonCarrotUsed"] = listMake($skill[Summon Carrot]);
    property_summons_to_skills["_summonAnnoyanceUsed"] = listMake($skill[summon annoyance]);
    property_summons_to_skills["_perfectFreezeUsed"] = listMake($skill[Perfect Freeze]);
    property_summons_to_skills["_communismUsed"] = listMake($skill[Communism!]);
    property_summons_to_skills["_preventScurvy"] = listMake(lookupSkill("Prevent Scurvy and Sobriety"));
    
    skills_to_title_notes[$skill[summon annoyance]] = get_property_int("summonAnnoyanceCost") + " swagger";
    
    
    
    
    
    if (my_path().id == PATH_AVATAR_OF_SNEAKY_PETE) {
        property_summons_to_skills["_petePartyThrown"] = listMake($skill[Throw Party]);
        property_summons_to_skills["_peteRiotIncited"] = listMake($skill[Incite Riot]);
        
        int audience_max = 30;
        int hate_useful_max = 25; //ashes and soda max out early; more audience hatred only gives crates and grenades, not of absolute importance
        if ($item[Sneaky Pete's leather jacket].equipped_amount() > 0 || $item[Sneaky Pete's leather jacket (collar popped)].equipped_amount() > 0) {
            audience_max = 50;
            hate_useful_max = 41;
        }
            
        if (my_audience() < audience_max)
            skills_to_details[$skill[Throw Party]] = "Ideally have " + audience_max + " audience love before casting.";
        else
            skills_to_details[$skill[Throw Party]] = "Gain party supplies.";
        
        if (my_audience() > -hate_useful_max)
            skills_to_details[$skill[Incite Riot]] = "Ideally have " + hate_useful_max + " audience hate before casting.";
        else
            skills_to_details[$skill[Incite Riot]] = "This fire is out of control";
    }
    if (my_path().id == PATH_AVATAR_OF_JARLSBERG) {
        property_summons_to_skills["_jarlsCreamSummoned"] = listMake($skill[Conjure Cream]);
        property_summons_to_skills["_jarlsEggsSummoned"] = listMake($skill[Conjure Eggs]);
        property_summons_to_skills["_jarlsDoughSummoned"] = listMake($skill[Conjure Dough]);
        property_summons_to_skills["_jarlsVeggiesSummoned"] = listMake($skill[Conjure Vegetables]);
        property_summons_to_skills["_jarlsCheeseSummoned"] = listMake($skill[Conjure Cheese]);
        property_summons_to_skills["_jarlsPotatoSummoned"] = listMake($skill[Conjure Potato]);
        property_summons_to_skills["_jarlsMeatSummoned"] = listMake($skill[Conjure Meat Product]);
        property_summons_to_skills["_jarlsFruitSummoned"] = listMake($skill[Conjure Fruit]);
    }
    if (my_path().id == PATH_AVATAR_OF_BORIS) {
        property_summons_to_skills["_demandSandwich"] = listMake($skill[Demand Sandwich]);
        property_summon_limits["_demandSandwich"] = 3;
    }
    
    property_summons_to_skills["_requestSandwichSucceeded"] = listMake($skill[Request Sandwich]);
    
    property_summons_to_skills["grimoire1Summons"] = listMake($skill[Summon Hilarious Objects]);
    property_summons_to_skills["grimoire2Summons"] = listMake($skill[Summon Tasteful Items]);
    property_summons_to_skills["grimoire3Summons"] = listMake($skill[Summon Alice's Army Cards]);
    property_summons_to_skills["_grimoireGeekySummons"] = listMake($skill[Summon Geeky Gifts]);
    if (mafiaIsPastRevision(14300)) {
        property_summons_to_skills["_grimoireConfiscatorSummons"] = listMake($skill[Summon Confiscated Things]);
        skills_to_urls[$skill[Summon Confiscated Things]] = "campground.php?action=bookshelf";
    }
    property_summons_to_skills["_candySummons"] = listMake($skill[Summon Crimbo Candy]);
    property_summons_to_skills["_summonResortPassUsed"] = listMake($skill[Summon Kokomo Resort Pass]);
    property_summons_to_skills["_incredibleSelfEsteemCast"] = listMake(lookupSkill("Incredible Self-Esteem"));
    skills_to_details[lookupSkill("Incredible Self-Esteem")] = "Gives or extends affirmation buffs.";
    if (__misc_state["in run"] && lookupItem("Daily Affirmation: Always be Collecting").available_amount() > 0 && lookupItem("Daily Affirmation: Always be Collecting").to_effect().have_effect() == 0)
        skills_to_details[lookupSkill("Incredible Self-Esteem")] += "|Possibly use Always be Collecting affirmation before casting.";
    
    foreach s in $skills[Summon Hilarious Objects,Summon Tasteful Items,Summon Alice's Army Cards,Summon Geeky Gifts]
        skills_to_urls[s] = "campground.php?action=bookshelf";
    


    int muscle_basestat = my_basestat($stat[muscle]);
    item summoned_knife = $item[none];
    if (muscle_basestat < 10)
        summoned_knife = $item[boot knife];
    else if (muscle_basestat < 20)
        summoned_knife = $item[broken beer bottle];
    else if (muscle_basestat < 40)
        summoned_knife = $item[sharpened spoon];
    else if (muscle_basestat < 60)
        summoned_knife = $item[candy knife];
    else
        summoned_knife = $item[soap knife];
    if (summoned_knife.available_amount() > 0 && summoned_knife != $item[none]) {
        //already have the knife, don't annoy them:
        //(or ask them to closet the knife?)
        remove property_summons_to_skills["_discoKnife"];
        //skills_to_details[$skill[that's not a knife]] = "Closet " + summoned_knife + " first.";
    }

    foreach property in property_summons_to_skills {
        if (property_summon_limits[property] != 0 && get_property_int(property) >= property_summon_limits[property] || get_property_boolean(property))
            continue;
        foreach key in property_summons_to_skills[property] {
            skill s = property_summons_to_skills[property][key];
            if (!s.skill_is_usable())
                continue;

            string line = s.to_string();
            string [int] description;
            if (s.mp_cost() > 0) {
                line += " (" + s.mp_cost() + " MP)";
                //description.listAppend(s.mp_cost() + " MP");
            }
            if (skills_to_title_notes contains s) {
                line += " (" + skills_to_title_notes[s] + " )";
            }
            string details = skills_to_details[s];
            if (details != "")
                description.listAppend(details);
                
                
            if (url.length() == 0) {
                if (skills_to_urls contains s)
                    url = skills_to_urls[s];
                else
                    url = "skills.php";
            }

            subentries.listAppend(ChecklistSubentryMake(line, "", description));
            break;
        }
    }

    if (subentries.count() > 0) {
        subentries.listPrepend(ChecklistSubentryMake("Skill summons:"));
        ChecklistEntry entry = ChecklistEntryMake("__item Knob Goblin love potion", url, subentries, importance);
        entry.tags.id = "Daily summon skills resource";
        entry.should_indent_after_first_subentry = true;
        resource_entries.listAppend(entry);
    }
    
    
    if (lookupSkill("Evoke Eldritch Horror").skill_is_usable() && !get_property_boolean("_eldritchHorrorEvoked")) {
        resource_entries.listAppend(ChecklistEntryMake("__skill Evoke Eldritch Horror", "skillz.php", ChecklistSubentryMake("Evoke Eldritch Horror", "", "Free fight."), 5).ChecklistEntrySetCombinationTag("daily free fight").ChecklistEntrySetIDTag("Evoke eldritch horror skill free fight"));
    }
    if (!get_property_boolean("_eldritchTentacleFought") && my_path().id != PATH_EXPLOSIONS && my_path().id != PATH_COMMUNITY_SERVICE) {
        resource_entries.listAppend(ChecklistEntryMake("__skill Evoke Eldritch Horror", "place.php?whichplace=forestvillage&action=fv_scientist", ChecklistSubentryMake("Science Tent Tentacle", "", "Free fight."), 5).ChecklistEntrySetCombinationTag("daily free fight").ChecklistEntrySetIDTag("Daily forest tentacle free fight"));
    }
    
}
