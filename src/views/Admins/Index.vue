<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const firstName = ref('');
const lastName = ref('');
const phoneNo = ref('');
const emailAddress = ref('');
const pincode = ref('');
const country = ref('India');
const state = ref('');
const city = ref('');
const roles = ref([]);
const adminSubmit = async (event) => {
    event.preventDefault();
    const adminData = {
        firstName: firstName.value,
        lastName: lastName.value,
        phoneNo: phoneNo.value,
        emailAddress: emailAddress.value,
        pincode: pincode.value,
        country: country.value,
        state: state.value,
        city: city.value
    }
    
    console.log('admin Data:', adminData);
    
    // TODO: Add your data saving logic here (e.g., API call)
}
const fetchRoles = async () => {
  try {
    const response = await axios.get("http://127.0.0.1:8000/api/roles");
    roles.value = response.data; 
    console.log(roles.value);
  } catch (error) {
    console.error("API Error:", error);
  }
};
onMounted(fetchRoles);
</script>
<template>
    <div>
        <div class="card">
        <div class="card-body">
            <div class="col">
                <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#exampleVerticallycenteredModal">+ New Admin</button>
                <!-- Modal New admin -->
                <div class="modal fade" id="exampleVerticallycenteredModal" tabindex="-1" aria-hidden="true">
                    <div class="modal-dialog modal-dialog-centered">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h5 class="modal-title">Add Admin</h5>
                                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                            </div>
                            <div class="modal-body">
                                <form class="row g-3" @submit.prevent="adminSubmit">
                                    <div class="col-md-6">
                                        <label for="inputLastName1" class="form-label">First Name <span class="text-danger">*</span></label>
                                        <div class="input-group"> <span class="input-group-text bg-transparent"><i class='bx bxs-user'></i></span>
                                            <input type="text" class="form-control border-start-0" id="inputLastName1" placeholder="First Name" v-model="firstName" >
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputLastName2" class="form-label">Last Name <span class="text-danger">*</span></label>
                                        <div class="input-group"> <span class="input-group-text bg-transparent"><i class='bx bxs-user'></i></span>
                                            <input type="text" class="form-control border-start-0" id="inputLastName2" placeholder="Last Name" v-model="lastName" >
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputPhoneNo" class="form-label">Phone No <span class="text-danger">*</span></label>
                                        <div class="input-group"> <span class="input-group-text bg-transparent"><i class='bx bxs-phone'></i></span>
                                            <input type="text" class="form-control border-start-0" id="inputPhoneNo" placeholder="Phone No" v-model="phoneNo" >
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputEmailAddress" class="form-label">Email Address <span class="text-danger">*</span></label>
                                        <div class="input-group"> <span class="input-group-text bg-transparent"><i class='bx bxs-envelope'></i></span>
                                            <input type="email" class="form-control border-start-0" id="inputEmailAddress" placeholder="Email Address" v-model="emailAddress" >
                                        </div>
                                    </div>
                            
                                    <div class="col-md-6">
                                        <label for="inputPincode" class="form-label">Pincode <span class="text-danger">*</span></label>
                                        <div class="input-group"> <span class="input-group-text bg-transparent"><i class='bx bxs-map'></i></span>
                                        <input type="text" class="form-control" id="inputPincode" placeholder="Enter Pincode" v-model="pincode" >
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputCountry" class="form-label">Role <span class="text-danger">*</span></label>
                                        <div class="input-group">
                                            <span class="input-group-text bg-transparent"><i class='bx bxs-globe'></i></span>
                                            <select class="form-select" id="inputCountry" v-model="country">
                                                <option v-for="role in roles" :key="role.id" :value="role.name">{{ role.name.charAt(0).toUpperCase() + role.name.slice(1) }}</option>
                                            </select>
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputCountry" class="form-label">Country <span class="text-danger">*</span></label>
                                        <div class="input-group">
                                            <span class="input-group-text bg-transparent"><i class='bx bxs-globe'></i></span>
                                            <select class="form-select" id="inputCountry" v-model="country" >
                                                <option value="India" selected>India</option>
                                                <option value="USA">USA</option>
                                                <option value="UK">UK</option>
                                                <option value="Canada">Canada</option>
                                                <!-- Add more countries as needed -->
                                            </select>
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputState" class="form-label">State <span class="text-danger">*</span></label>
                                        <div class="input-group">
                                            <span class="input-group-text bg-transparent"><i class='bx bxs-map'></i></span>
                                            <select class="form-select" id="inputState" v-model="state" >
                                                <option value="" selected>Select State</option>
                                                <option value="Maharashtra">Maharashtra</option>
                                                <option value="Karnataka">Karnataka</option>
                                                <option value="Delhi">Delhi</option>
                                                <option value="Tamil Nadu">Tamil Nadu</option>
                                                <!-- Add more states as needed -->
                                            </select>
                                        </div>
                                    </div>
                                    <div class="col-md-6">
                                        <label for="inputCity" class="form-label">City <span class="text-danger">*</span></label>
                                        <div class="input-group">
                                            <span class="input-group-text bg-transparent"><i class='bx bxs-building'></i></span>
                                            <select class="form-select" id="inputCity" v-model="city" >
                                                <option value="" selected>Select City</option>
                                                <option value="Mumbai">Mumbai</option>
                                                <option value="Bangalore">Bangalore</option>
                                                <option value="Delhi">Delhi</option>
                                                <option value="Chennai">Chennai</option>
                                                <!-- Add more cities as needed -->
                                            </select>
                                        </div>
                                    </div>
                                    <div class="modal-footer">
                                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                                        <button type="submit" class="btn btn-primary">Save</button>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <table class="table mb-0 table-striped">
                <thead>
                    <tr>
                        <th scope="col">#</th>
                        <th scope="col">First</th>
                        <th scope="col">Last</th>
                        <th scope="col">Handle</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <th scope="row">1</th>
                        <td>Mark</td>
                        <td>Otto</td>
                        <td>@mdo</td>
                    </tr>
                    <tr>
                        <th scope="row">2</th>
                        <td>Jacob</td>
                        <td>Thornton</td>
                        <td>@fat</td>
                    </tr>
                    <tr>
                        <th scope="row">3</th>
                        <td colspan="2">Larry the Bird</td>
                        <td>@twitter</td>
                    </tr>
                </tbody>
            </table>
        </div>
		</div>
    </div>
</template>