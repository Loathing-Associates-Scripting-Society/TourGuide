//Crepe Parachute
RegisterTaskGenerationFunction("CrepeParachuteGenerateTasks");
void CrepeParachuteGenerateTasks(ChecklistEntry [int] task_entries, ChecklistEntry [int] optional_task_entries, ChecklistEntry [int] future_task_entries)
{
    if ($item[crepe paper parachute cape].available_amount() == 0) return;

    string url = "inventory.php?action=parachute&pwd=" + my_hash();
    // Beige Map
    if ($effect[Everything Looks Beige].have_effect() == 0)
    {
        string [int] description;
        description.listAppend(HTMLGenerateSpanFont("It's mapparachute time!", "orange"));
        task_entries.listAppend(ChecklistEntryMake("__item crepe paper parachute cape", url, ChecklistSubentryMake("Crepe Parachute ready", "", description), -11));
    }
}
