// ===============================
// Waste Pickup Scheduler
// Part 1 - Data & Pickup Handling
// ===============================

// Load pickups from Local Storage
let pickups = JSON.parse(localStorage.getItem("pickups")) || [];

// Load feedback from Local Storage
let feedbacks = JSON.parse(localStorage.getItem("feedbacks")) || [];

// Save pickups
function savePickups() {
    localStorage.setItem("pickups", JSON.stringify(pickups));
}

// Save feedback
function saveFeedbackData() {
    localStorage.setItem("feedbacks", JSON.stringify(feedbacks));
}

// Pickup Form
const pickupForm = document.getElementById("pickupForm");

if (pickupForm) {
    pickupForm.addEventListener("submit", function (e) {

        e.preventDefault();

        const pickup = {
            id: Date.now(),
            name: document.getElementById("name").value,
            phone: document.getElementById("phone").value,
            address: document.getElementById("address").value,
            wasteType: document.getElementById("wasteType").value,
            date: document.getElementById("date").value,
            time: document.getElementById("time").value,
            status: "pending"
        };

        pickups.push(pickup);

        savePickups();

        displayPickups();

        updateDashboard();

        alert("Pickup scheduled successfully!");

        pickupForm.reset();
    });
}

// Display Pickups
function displayPickups() {

    const pickupList = document.getElementById("pickupList");

    if (!pickupList) return;

    pickupList.innerHTML = "";

    pickups.forEach((pickup) => {

        pickupList.innerHTML += `
            <div class="card">

                <h3>${pickup.name}</h3>

                <p><strong>Phone:</strong> ${pickup.phone}</p>

                <p><strong>Address:</strong> ${pickup.address}</p>

                <p><strong>Waste:</strong> ${pickup.wasteType}</p>

                <p><strong>Date:</strong> ${pickup.date}</p>

                <p><strong>Time:</strong> ${pickup.time}</p>

                <p><strong>Status:</strong> ${pickup.status}</p>

                <button onclick="completePickup(${pickup.id})">
                    Complete
                </button>

                <button onclick="deletePickup(${pickup.id})">
                    Delete
                </button>

            </div>
        `;
    });
}
// ===============================
// Waste Pickup Scheduler
// Part 1 - Data & Pickup Handling
// ===============================

// Load pickups from Local Storage
let pickups = JSON.parse(localStorage.getItem("pickups")) || [];

// Load feedback from Local Storage
let feedbacks = JSON.parse(localStorage.getItem("feedbacks")) || [];

// Save pickups
function savePickups() {
    localStorage.setItem("pickups", JSON.stringify(pickups));
}

// Save feedback
function saveFeedbackData() {
    localStorage.setItem("feedbacks", JSON.stringify(feedbacks));
}

// Pickup Form
const pickupForm = document.getElementById("pickupForm");

if (pickupForm) {
    pickupForm.addEventListener("submit", function (e) {

        e.preventDefault();

        const pickup = {
            id: Date.now(),
            name: document.getElementById("name").value,
            phone: document.getElementById("phone").value,
            address: document.getElementById("address").value,
            wasteType: document.getElementById("wasteType").value,
            date: document.getElementById("date").value,
            time: document.getElementById("time").value,
            status: "pending"
        };

        pickups.push(pickup);

        savePickups();

        displayPickups();

        updateDashboard();

        alert("Pickup scheduled successfully!");

        pickupForm.reset();
    });
}

// Display Pickups
function displayPickups() {

    const pickupList = document.getElementById("pickupList");

    if (!pickupList) return;

    pickupList.innerHTML = "";

    pickups.forEach((pickup) => {

        pickupList.innerHTML += `
            <div class="card">

                <h3>${pickup.name}</h3>

                <p><strong>Phone:</strong> ${pickup.phone}</p>

                <p><strong>Address:</strong> ${pickup.address}</p>

                <p><strong>Waste:</strong> ${pickup.wasteType}</p>

                <p><strong>Date:</strong> ${pickup.date}</p>

                <p><strong>Time:</strong> ${pickup.time}</p>

                <p><strong>Status:</strong> ${pickup.status}</p>

                <button onclick="completePickup(${pickup.id})">
                    Complete
                </button>

                <button onclick="deletePickup(${pickup.id})">
                    Delete
                </button>

            </div>
        `;
    });
}
// ===============================
// Part 3 - Feedback & Initialization
// ===============================

// Save Feedback
function saveFeedback() {

    const name = document.getElementById("feedbackName").value;
    const rating = document.getElementById("rating").value;
    const comment = document.getElementById("comment").value;

    if (!name || !rating || !comment) {
        alert("Please complete all feedback fields.");
        return;
    }

    feedbacks.push({
        name,
        rating,
        comment,
        date: new Date().toLocaleString()
    });

    saveFeedbackData();

    displayFeedback();

    document.getElementById("feedbackName").value = "";
    document.getElementById("rating").value = "";
    document.getElementById("comment").value = "";

    alert("Thank you for your feedback!");
}

// Display Feedback
function displayFeedback() {

    const feedbackList = document.getElementById("feedbackList");

    if (!feedbackList) return;

    feedbackList.innerHTML = "";

    feedbacks.forEach(item => {

        feedbackList.innerHTML += `
            <div class="card">
                <h3>${item.name}</h3>
                <p>${item.rating}</p>
                <p>${item.comment}</p>
                <small>${item.date}</small>
            </div>
        `;

    });

}

// Pickup Reminder
function checkTodayReminder() {

    const today = new Date().toISOString().split("T")[0];

    const todayPickups = pickups.filter(
        pickup => pickup.date === today &&
        pickup.status === "pending"
    );

    if (todayPickups.length > 0) {

        alert(
            "Reminder: You have " +
            todayPickups.length +
            " pickup(s) scheduled for today."
        );

    }

}

// ===============================
// App Initialization
// ===============================

displayPickups();
displayFeedback();
updateDashboard();
checkTodayReminder();
