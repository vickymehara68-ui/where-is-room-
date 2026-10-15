# where-is-room-

import streamlit as st

st.set_page_config(
    page_title="Where Is Room?",
    page_icon="🏠",
    layout="centered"
)

st.title("🏠 Where Is Room?")
st.subheader("Students ke liye Room, PG aur Hostel Finder")
st.write("Apne budget mein rehne ki jagah khojiye!")

# Demo listings: ye asli verified rooms nahi hain
rooms = [
    {
        "city": "Purnia",
        "name": "Student Room Center",
        "type": "Room",
        "rent": 2500,
        "location": "Line Bazar",
        "facilities": "Bed, Fan, Wi-Fi"
    },
    {
        "city": "Purnia",
        "name": "Shanti Student PG",
        "type": "PG",
        "rent": 3500,
        "location": "Madhubani",
        "facilities": "Food, Water, Wi-Fi"
    },
    {
        "city": "Patna",
        "name": "Student Hostel",
        "type": "Hostel",
        "rent": 4000,
        "location": "Boring Road",
        "facilities": "Bed, Food, Wi-Fi"
    },
    {
        "city": "Delhi",
        "name": "Campus Stay",
        "type": "Hostel",
        "rent": 6000,
        "location": "Mukherjee Nagar",
        "facilities": "Bed, Study Table, Wi-Fi"
    }
]

city = st.text_input(
    "📍 Apna city likhein",
    placeholder="Jaise Purnia"
)

room_type = st.selectbox(
    "🏡 Room ka type",
    ["Sabhi", "Room", "PG", "Hostel"]
)

budget = st.slider(
    "💰 Maximum monthly rent (₹)",
    1000, 20000, 5000, step=500
)

if st.button("🔍 Search Room", type="primary"):
    results = [
        room for room in rooms
        if (not city or
            city.strip().lower() in room["city"].lower())
        and (room_type == "Sabhi" or
             room["type"] == room_type)
        and room["rent"] <= budget
    ]

    if results:
        st.success(f"{len(results)} listings mili!")

        for room in results:
            with st.container(border=True):
                st.subheader("🏠 " + room["name"])
                st.write("📍 City:", room["city"])
                st.write("Location:", room["location"])
                st.write("Type:", room["type"])
                st.write(f"💰 Rent: ₹{room['rent']}/month")
                st.write("Facilities:", room["facilities"])
    else:
        st.warning(
            "Room nahi mila. City ya budget badal kar dekhein."
        )

st.divider()
st.caption(
    "Where Is Room? | Demo Version | "
    "Room aur owner ki details verify karein."
)
