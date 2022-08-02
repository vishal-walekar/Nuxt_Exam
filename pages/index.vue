<template>
<main class="flex justify-center">
    <div class="p-2">

        <h2 class="text-teal-900  text-center font-bold text-4xl pt-6">Hospital Management</h2>
        <hr />
        <br />

        <div>
            <div><label class="font-bold text-xl"> Select your slots: </label>
                <button class="py-1 border-4  bg-blue-200 hover:bg-blue-400 border-black" @click="showSlots">click here to show</button></div>
            <div class="bg-fuchsia-300 border-4 border-black w-1/10" v-for="item in timeSlots">


                <tr v-for="(item, i) in myarr" :key="item">
                <td class="px-4 border-black rounded-lg border-2">{{item.id = i+1}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.firstname}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.number}}</td>
                 </tr>

                <div class="font-bold text-xl p-5">Start Time {{item.startTime }}</div>
                <div class="font-bold text-xl p-5">End Time {{ item.endTime }}</div>

                <div>
                    <button @click="display" class="py-2 px-10 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3">
                        <label for="firstname"> Book now </label>

                    </button>
                   
                </div>
                
            </div>
        </div>

        <form action=" "></form>
        <form v-if="formshow == true" @submit="customSubmit" class="bg-gray-100 border-black rounded-lg border-2 px-12 ">
            <table class="grid  content-center">
                <h2 class="text-teal-900  text-center font-bold text-4xl pt-6">Registration Form </h2>
                <h3 class="text-teal-900  text-center font-bold pt-6">Book slots for a hospital.</h3>
                <br />
                <hr />
                <br />
                <label class="font-bold text-xl" for="firstname">Name:</label>
                <input @change="validationName" type="text" v-model="user.firstname" id="firstname" name="firstname" placeholder="Enter your full name" required />

                <label class="font-bold text-xl pt-3" for="number">Phone Number: </label>
                <input @change="namecheck" type="number" v-model="user.number" id="number" name="number" placeholder="Enter your number" required/>

                <div class="text-center pt-10">
                    <button class="py-2 px-10 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3" type="submit" @click="customSubmit"> Submit </button>

                    <button class="py-2 px-10 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3" type="reset"> Reset </button>

                </div>
            </table>
        </form>
        <br>
        <table v-if="formshow == true" class="list">
            <h1 class="text-teal-900 text-xl font-bold pt-1"> Booked slots</h1>
            <tr>
                <th class="px-4 border-black rounded-lg border-2">Id</th>
                <th class="px-4 border-black rounded-lg border-2">Name</th>
                <th class="px-4 border-black rounded-lg border-2">Number</th>
                <th class="px-4 border-black rounded-lg border-2">Booking time</th>
                <th class="px-4 border-black rounded-lg border-2">Action</th>
            </tr>

            <tr v-for="(item, i) in myarr" :key="item">
                <td class="px-4 border-black rounded-lg border-2">{{item.id = i+1}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.firstname}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.number}}</td>

                <td class="px-4 border-black rounded-lg border-2">{{item. startTime}}</td>

                <td class="px-4 border-black rounded-lg border-2">
                    <button class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md " type="delete" @click="customDelete(i)"> Slot Delete </button>
                    <button  class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md" type="edit" @click="customEdit(i)" for="firstname">  Edit Details </button>

                </td>

            </tr>

        </table>
    </div>
</main>
</template>

<script>
export default {
    data() {
        return {
            isEdit: false,
            formshow: false,
            formhide:false,
            indexEdit: -1,
            myarr: [],
            timeSlots: [],

            user: {
                id: 0,
                firstname: '',
                number: '',
                date: '',
                time: '',
            },

        };
    },
    methods: {

        customSubmit(event) {
            event.preventDefault();

            if (this.isEdit == true) {
                this.myarr[this.indexEdit] = this.user;
                this.isEdit = false;
                this.indexEdit = -1;
            } else {
                this.myarr.push(this.user);
            }
            this.hideform();

            this.user = {
                id: 0,
                firstname: '',
                number: '',
                date: '',
                time: '',
            };

        },
        customDelete(index) {
            this.myarr.splice(index, 1);

        },
        customEdit(index) {
            this.user.firstname = this.myarr[index].firstname;
            this.user.number = this.myarr[index].number;
            this.user.date = this.myarr[index].date;
            // this.user.time = this.myarr[index].time;

            this.isEdit = true;
            this.indexEdit = index;

        },
        showSlots() {
            var d;
            var e;
            d = new Date("2022-08-01 08:50:00");
            e = new Date("2022-08-01 09:00:00");
            for (let i = 0; i < 20; i++) {
                d.setMinutes(d.getMinutes() + 10);
                e.setMinutes(d.getMinutes() + 10);
                // console.log(d);
                this.timeSlots.push({
                    startTime: d.toLocaleTimeString(),
                    endTime: e.toLocaleTimeString(),
                });
            }
            //console.log(d);
        },
        display() {
            this.formshow = true;
        },

        hideform(){
            this.formshow=false;
        },

        validationName() {
            if (!isNaN(this.user.firstname) || this.user.firstname == null || this.user.firstname == "") {
                alert("Please Enter Name");
                // console.log("Please Enter Name");
                this.resetForm();
            } else {
                console.log(this.user.firstname);
                // alert("Name is valid");
            }
        },
        namecheck() {
            if (isNaN(this.user.number) || this.user.number < 1000000000 || this.user.number > 9999999999) {
                alert("Mobile Number is Invalid");
                this.resetForm();
            } else {
                // alert("Mobile Number is valid");
            }
        }
    }
}
</script>
