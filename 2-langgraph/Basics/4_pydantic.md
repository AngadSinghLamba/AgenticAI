# **📌 What is Pydantic?**
Pydantic is a **data validation and settings management** library for Python that enforces **type safety and validation** using Python’s **type hints**.

🔹 **Official Docs**: [Pydantic](https://docs.pydantic.dev/latest/)  

---

## **🚀 Why Use Pydantic?**
✔ **Automatic Data Validation** – Ensures values match expected types.  
✔ **Error Handling** – Provides **clear, human-readable error messages**.  
✔ **Auto-Parsing** – Converts **JSON, strings, and other types** automatically.  
✔ **Configurable** – Works for **API requests, form validation, and more**.  
✔ **Fast and Lightweight** – Built using **Cython**, making it **super fast**.

---

## **📌 Basic Example**
```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
    email: str

# ✅ Valid Data
user = User(name="Alice", age=30, email="alice@example.com")
print(user)  # User(name='Alice', age=30, email='alice@example.com')

# ❌ Invalid Data (Type Error)
user = User(name="Bob", age="thirty", email="bob@example.com")
# ValidationError: 'thirty' is not a valid integer.
```
✔ **Automatically validates data and raises errors if types don’t match.**

---

## **📌 Pydantic Auto-Converts Data Types**
Pydantic **automatically converts valid values** into the correct type.

```python
class Product(BaseModel):
    name: str
    price: float
    in_stock: bool

product = Product(name="Laptop", price="999.99", in_stock="true")
print(product)  
# ✅ Output: Product(name='Laptop', price=999.99, in_stock=True)
```
✔ **Price (`"999.99"`) converted to `float`**  
✔ **In_stock (`"true"`) converted to `bool`**

---

## **📌 Handling Default Values**
```python
class Config(BaseModel):
    debug: bool = False  # Default value
    timeout: int = 30    # Default timeout is 30 seconds

config = Config()
print(config)  
# ✅ Output: Config(debug=False, timeout=30)
```
✔ **If values are missing, Pydantic assigns defaults.**

---

## **📌 Field Validation & Custom Constraints**
Use **`Field`** to set **constraints like min/max values, regex, and defaults**.

```python
from pydantic import BaseModel, Field

class User(BaseModel):
    name: str = Field(..., min_length=3, max_length=20)
    age: int = Field(..., ge=18, le=100)  # Age must be between 18-100
    email: str = Field(..., regex=r'^\S+@\S+\.\S+$')  # Must be a valid email

user = User(name="John", age=25, email="john@example.com")
print(user)
```
✔ **Ensures name length, age range, and valid email format.**

---

## **📌 Nested Models**
Pydantic allows **nested models** for complex data structures.

```python
class Address(BaseModel):
    city: str
    zip_code: str

class User(BaseModel):
    name: str
    address: Address

user = User(name="Alice", address={"city": "New York", "zip_code": "10001"})
print(user)
```
✔ **Automatically converts `dict` into an `Address` model.**

---

## **📌 Using Pydantic with FastAPI**
Pydantic is the **core of FastAPI** for request validation.

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class User(BaseModel):
    name: str
    age: int

@app.post("/users/")
async def create_user(user: User):
    return {"message": f"User {user.name} created!"}
```
✔ **Validates API request data automatically!** 🚀

---

## **📌 When to Use Pydantic?**
| **Use Case** | **Why Use Pydantic?** |
|-------------|------------------|
| **API Input Validation** | Ensures valid request data in **FastAPI, Flask, Django**. |
| **Configuration Management** | Loads & validates settings from `.env` or `JSON`. |
| **Data Parsing & Cleaning** | Auto-converts values like `"true"` → `True`. |
| **Database Models** | Works with **SQLAlchemy, MongoDB, and ORMs**. |

---

## **🔥 Final Thoughts**
🚀 **Pydantic makes Python data validation easy, fast, and reliable.**  
🚀 **Perfect for APIs, data processing, and structured input validation.**  
