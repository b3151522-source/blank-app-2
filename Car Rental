import streamlit as st

class Car:
    def __init__(self, car_id, model, year):
        self.car_id = car_id
        self.model = model
        self.year = year
        self.rented = False
        self.renter_name = None

    def __str__(self):
        status = "مؤجرة" if self.rented else "متوفرة"
        return f"ID: {self.car_id} | {self.model} ({self.year}) | {status}"

class CarRentalSystem:
    def __init__(self):
        self.cars = []
        self.next_id = 1

    def add_car(self, model, year):
        car = Car(self.next_id, model, year)
        self.cars.append(car)
        self.next_id += 1

    def list_cars(self, only_available=None):
        return [
            car for car in self.cars
            if only_available is None or (car.rented != only_available)
        ]

    def rent_car(self, car_id, renter_name):
        for car in self.cars:
            if car.car_id == car_id and not car.rented:
                car.rented = True
                car.renter_name = renter_name
                return True
        return False

    def return_car(self, car_id):
        for car in self.cars:
            if car.car_id == car_id and car.rented:
                car.rented = False
                car.renter_name = None
                return True
        return False

    def delete_car(self, car_id):
        for i, car in enumerate(self.cars):
            if car.car_id == car_id and not car.rented:
                del self.cars[i]
                return True
        return False

# إنشاء النظام وتخزينه في session_state
if 'system' not in st.session_state:
    st.session_state.system = CarRentalSystem()

st.title("نظام تأجير السيارات")

# إضافة سيارة
st.header("إضافة سيارة جديدة")
model = st.text_input("موديل السيارة")
year = st.text_input("سنة الصنع")
if st.button("إضافة"):
    if model and year:
        st.session_state.system.add_car(model, year)
        st.success("تمت إضافة السيارة بنجاح.")

# عرض جميع السيارات
st.header("جميع السيارات")
for car in st.session_state.system.list_cars():
    st.write(str(car))

# تأجير سيارة
st.header("تأجير سيارة")
car_id_rent = st.number_input("رقم السيارة للتأجير", min_value=1, step=1)
renter_name = st.text_input("اسم المستأجر")
if st.button("تأجير"):
    if st.session_state.system.rent_car(car_id_rent, renter_name):
        st.success("تم تأجير السيارة.")
    else:
        st.error("تعذر تأجير السيارة.")

# إرجاع سيارة
st.header("إرجاع سيارة")
car_id_return = st.number_input("رقم السيارة للإرجاع", min_value=1, step=1, key="return")
if st.button("إرجاع"):
    if st.session_state.system.return_car(car_id_return):
        st.success("تم إرجاع السيارة.")
    else:
        st.error("تعذر إرجاع السيارة.")

# حذف سيارة
st.header("حذف سيارة")
car_id_delete = st.number_input("رقم السيارة للحذف", min_value=1, step=1, key="delete")
if st.button("حذف"):
    if st.session_state.system.delete_car(car_id_delete):
        st.success("تم حذف السيارة.")
    else:
        st.error("تعذر حذف السيارة.")# Ass
As
