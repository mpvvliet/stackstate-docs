---
title: Script API - UI
kind: Documentation
---

# ui

This script API contains functions that allow the user-interface of StackState to take some actions. These functions only work in the context of scripts that are executed by a user from the user-interface. [Component actions](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/configure/component_actions/README.md) are an example of scripts that can trigger actions in the user-interface.

## Function: `showReport`

Shows a report in the user-interface. The user-interface will open a dialog with the report in it.

**Args:**

* `reportName` - Name of the report. In a dialog with the report, the name of the report will be in the title bar.
* `stmlContent` - The report markup. See [StackState Markup Language](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/develop/stml/README.md) for more information on how to format a report.
* Optional `data` - A map with data elements that can be referenced by the STML.

**Return type:**

* Async: ShowStmlReport

**Examples:**

The following example will show a nice shopping list report:

```text
UI.showReport(
    "My shopping list",
    """# To buy
    | Bring *report*.
    |  * Apples
    |  * Oranges
    """.stripMargin()
)
```

Please note the `.stripMargin()` call. This is a Groovy function for strings that strips leading whitespace/control characters followed by '\|' from every line. This way indenting can be retained without introducing leading whitespace in the STML.

## Function: `showTopologyByQuery`

Sets the user-interface to the topology perspective and changes the SQTL query.

If the user is currently in an unsaved view, the user receives a prompt dialog asking whether they are okay in navigating to another part of the topology. If the user continues the action they will loose their current view.

**Args:**

* `query` - [STQL query](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/use/topology_selection_advanced/README.md) that selects what part of the topology is shown.

**Return type:**

* Async: ShowTopologyByQuery

**Examples:**

Redirects the user-interface to show the Azure topology.

```text
UI.showTopologyByQuery('domain IN ("Azure")')
```

## Function: `redirectToURL`

Opens a new tab in the user's browser to some URL.

**Args:**

* `url` - the URL to redirect the browser to.

**Return type:**

* Async: URLRedirectResponse

**Examples:**

Open the stackstate.com website in a new tab in the browser.

```text
UI.redirectToUrl("http://wwww.stackstate.com")
```

