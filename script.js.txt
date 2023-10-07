document.addEventListener("DOMContentLoaded", function () {
    // Get the current day of the week (0 = Sunday, 1 = Monday, ..., 6 = Saturday)
    var today = new Date().getDay();
    var dayNames = ["sunday", "monday", "tuesday", "wednesday", "thursday", "friday", "saturday"];
    var currentDay = dayNames[today];
    
    // Check if there are stored checkbox states for the current day
    if (localStorage[currentDay]) {
        var checkboxes = JSON.parse(localStorage[currentDay]);
        
        // Check the checkboxes based on the stored states
        checkboxes.forEach(function (checkboxId) {
            var checkbox = document.getElementById(checkboxId);
            if (checkbox) {
                checkbox.checked = true;
            }
        });
    }
    
    // Add event listeners to store checkbox states when they change
    var checkboxes = document.querySelectorAll('input[type="checkbox"]');
    checkboxes.forEach(function (checkbox) {
        checkbox.addEventListener('change', function () {
            var checkedCheckboxes = Array.from(checkboxes)
                .filter((checkbox) => checkbox.checked)
                .map((checkbox) => checkbox.id);
            localStorage[currentDay] = JSON.stringify(checkedCheckboxes);
        });
    });
});
