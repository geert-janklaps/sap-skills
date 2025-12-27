# Compass for Seamless Planning

New in SAC Q4 2025: Enhanced planning integration with Compass support for seamless workflows.

---

## Overview

Compass provides a unified planning experience that integrates planning operations across stories, enabling seamless workflows with enhanced version management and approval processes.

**Availability**: SAC Q4 2025 (2025.21)
**Requires**: Planning-enabled models, BPC or SAC Planning license

---

## Key Concepts

### Seamless Versions

Seamless versions allow continuous planning without explicit version switching:

- **Auto-save**: Changes saved automatically to seamless version
- **No Lock Required**: Multiple users can edit simultaneously
- **Conflict Resolution**: Built-in merge capabilities

### Planning Workflows

Structured approval processes:

- **Submit**: Submit data for review
- **Approve/Reject**: Reviewer actions
- **Publish**: Final publication to public version

---

## API Reference

### getSeamlessVersion()

Get the seamless version for the current planning context.

```javascript
var planning = Table_1.getPlanning();
var seamlessVersion = planning.getSeamlessVersion();

if (seamlessVersion !== null) {
    console.log("Seamless version:", seamlessVersion.id);
}
```

### isSeamlessEnabled()

Check if seamless planning is enabled for the model.

```javascript
var planning = Table_1.getPlanning();

if (planning.isSeamlessEnabled()) {
    // Use seamless planning APIs
} else {
    // Fall back to traditional version management
}
```

### submitForApproval(options)

Submit current planning data for approval.

```javascript
var planning = Table_1.getPlanning();

Application.showBusyIndicator("Submitting for approval...");

try {
    planning.submitForApproval({
        comment: "Q4 forecast ready for review",
        notifyReviewers: true
    });

    Application.showMessage(
        ApplicationMessageType.Success,
        "Submitted for approval"
    );
} catch (e) {
    Application.showMessage(
        ApplicationMessageType.Error,
        "Submit failed: " + e.message
    );
} finally {
    Application.hideBusyIndicator();
}
```

### checkApprovalStatus()

Get the current approval status.

```javascript
var planning = Table_1.getPlanning();
var status = planning.checkApprovalStatus();

console.log("Status:", status.state); // "pending", "approved", "rejected"
console.log("Reviewer:", status.reviewer);
console.log("Comments:", status.comments);

// Update UI based on status
switch (status.state) {
    case "pending":
        Text_Status.setText("Awaiting approval");
        break;
    case "approved":
        Text_Status.setText("Approved by " + status.reviewer);
        break;
    case "rejected":
        Text_Status.setText("Rejected: " + status.comments);
        break;
}
```

### approveSubmission(options)

Approve a pending submission (reviewer only).

```javascript
var planning = Table_1.getPlanning();

planning.approveSubmission({
    comment: "Approved - numbers look good",
    publishImmediately: true
});
```

### rejectSubmission(options)

Reject a pending submission (reviewer only).

```javascript
var planning = Table_1.getPlanning();

planning.rejectSubmission({
    comment: "Please review Q4 assumptions",
    notifySubmitter: true
});
```

---

## Workflow Implementation

### Complete Planning Workflow

```javascript
// Step 1: Initialize seamless planning session
function initializeSeamlessPlanning() {
    var planning = Table_1.getPlanning();

    if (!planning.isSeamlessEnabled()) {
        Application.showMessage(
            ApplicationMessageType.Warning,
            "Seamless planning not available for this model"
        );
        return false;
    }

    var seamless = planning.getSeamlessVersion();
    if (seamless === null) {
        planning.createSeamlessVersion();
    }

    return true;
}

// Step 2: Save work (auto-save enabled, but manual option)
function saveProgress() {
    var planning = Table_1.getPlanning();

    planning.saveSeamlessChanges({
        comment: "Work in progress - " + new Date().toLocaleString()
    });

    Application.showMessage(
        ApplicationMessageType.Info,
        "Progress saved"
    );
}

// Step 3: Submit for approval
function submitForReview() {
    var planning = Table_1.getPlanning();

    // Validate before submission
    if (!validatePlanningData()) {
        Application.showMessage(
            ApplicationMessageType.Error,
            "Please fix validation errors before submitting"
        );
        return;
    }

    planning.submitForApproval({
        comment: InputField_Comment.getValue(),
        notifyReviewers: true
    });
}

// Step 4: Check status
function refreshStatus() {
    var planning = Table_1.getPlanning();
    var status = planning.checkApprovalStatus();

    updateStatusDisplay(status);
    updateButtonStates(status);
}
```

### Status Display Helper

```javascript
function updateStatusDisplay(status) {
    var statusText = "";
    var statusColor = "";

    switch (status.state) {
        case "draft":
            statusText = "Draft - Not Submitted";
            statusColor = "#666666";
            break;
        case "pending":
            statusText = "Pending Approval";
            statusColor = "#FFA500";
            break;
        case "approved":
            statusText = "Approved";
            statusColor = "#008000";
            break;
        case "rejected":
            statusText = "Rejected - Revisions Needed";
            statusColor = "#FF0000";
            break;
        case "published":
            statusText = "Published";
            statusColor = "#0000FF";
            break;
    }

    Text_Status.setText(statusText);
    // Panel_Status.setBackgroundColor(statusColor);
}
```

---

## Conflict Resolution

### Handling Merge Conflicts

```javascript
var planning = Table_1.getPlanning();

try {
    planning.mergeSeamlessChanges();
} catch (e) {
    if (e instanceof MergeConflictError) {
        // Handle conflicts
        var conflicts = e.getConflicts();

        conflicts.forEach(function(conflict) {
            console.log("Conflict:", conflict.dimension, conflict.member);
            console.log("Your value:", conflict.localValue);
            console.log("Their value:", conflict.remoteValue);
        });

        // Show conflict resolution UI
        Application.openPopup(Popup_ConflictResolution);
    } else {
        throw e;
    }
}
```

### Resolve Individual Conflicts

```javascript
// In conflict resolution popup
function resolveConflict(conflictId, resolution) {
    var planning = Table_1.getPlanning();

    planning.resolveConflict(conflictId, {
        useValue: resolution // "local", "remote", or specific value
    });
}

// Resolve all with one choice
function resolveAllConflicts(resolution) {
    var planning = Table_1.getPlanning();

    planning.resolveAllConflicts({
        useValue: resolution // "local" or "remote"
    });

    Application.closePopup(Popup_ConflictResolution);
}
```

---

## Best Practices

1. **Check Seamless Support**: Always verify `isSeamlessEnabled()` before using seamless APIs
2. **Validate Before Submit**: Run validation before `submitForApproval()`
3. **Handle Conflicts Gracefully**: Implement conflict resolution UI
4. **Provide Status Feedback**: Keep users informed of workflow state
5. **Test Multi-User Scenarios**: Verify behavior with concurrent users

---

## Error Handling

```javascript
try {
    planning.submitForApproval({...});
} catch (e) {
    if (e instanceof ValidationError) {
        Application.showMessage(ApplicationMessageType.Error,
            "Validation failed: " + e.message);
    } else if (e instanceof WorkflowError) {
        Application.showMessage(ApplicationMessageType.Error,
            "Workflow error: " + e.message);
    } else if (e instanceof PermissionError) {
        Application.showMessage(ApplicationMessageType.Error,
            "Permission denied: " + e.message);
    } else {
        throw e;
    }
}
```

---

**Version**: Q4 2025 (2025.21)
**Last Updated**: 2025-12-27
