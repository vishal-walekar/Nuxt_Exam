<template>
<main class="flex justify-center">
    <div class="p-2">
        <form action="/first_page.vue"></form>
        <form @submit="customSubmit" class="bg-gray-100 border-black rounded-lg border-2 px-12 ">
            <table class="grid  content-center">
                <h2 class="text-teal-900  text-center font-bold text-4xl pt-6">Registration Form </h2>
                <h3 class="text-teal-900  text-center font-bold pt-6">Book slots for a hospital.</h3>
                <br />
                <hr />
                <br />
                <label class="font-bold text-xl" for="firstname">Name:</label>
                <input type="text" v-model="user.firstname" id="firstname" name="firstname" placeholder="Enter your full name" required />

                <label class="font-bold text-xl pt-3" for="number">Phone Number: </label>
                <input type="number" v-model="user.number" id="number" name="number" placeholder="Enter your number" />

                <label class="font-bold text-xl" for="date">Data</label>
                <input type="date" v-model="user.date" id="date" name="date" placeholder="dd-mm-yyyy" min="2022-08-01" max="2023-08-" />
                
                    <label class="font-bold text-xl" for="date">Selected Time Slot Time</label>
                    <input type="time" v-model="user.time" id="time" name="time" min="9:00" />
               
                <!-- <div class="pt-3">
                    <label class="font-bold text-xl pt-3" for="time"> Selected Time Slot 1: </label>
                    <div>

                        <select v-model="user.time">
                            <option>select</option>

                            <option>9:00 To 9:10</option>
                            <option>9:10 To 9:20</option>
                            <option>9:20 To 9:30</option>
                            <option>9:30 To 9:40</option>
                            <option>9:40 To 9:50</option>
                            <option>9:50 To 10:00</option>

                            <option>10:00 To 10:10</option>
                            <option>10:10 To 10:20</option>
                            <option>10:20 To 10:30</option>
                            <option>10:30 To 10:40</option>
                            <option>10:40 To 10:50</option>
                            <option>10:50 To 11:00</option>

                            <option>11:00 To 11:10</option>
                            <option>11:10 To 11:20</option>
                            <option>11:20 To 11:30</option>
                            <option>11:30 To 11:40</option>
                            <option>11:40 To 11:50</option>
                            <option>11:50 To 12:00</option>

                            <option>12:00 To 12:10</option>
                            <option>12:10 To 12:20</option>
                            <option>12:20 To 12:30</option>
                            <option>12:30 To 12:40</option>
                            <option>12:40 To 11:50</option>
                            <option>12:50 To 1:00</option>

                            <option>1:00 To 1:10</option>
                            <option>1:10 To 1:20</option>
                            <option>1:20 To 1:30</option>
                            <option>1:30 To 1:40</option>
                            <option>1:40 To 1:50</option>
                            <option>1:50 To 2:00</option>

                            <option>2:00 To 2:10</option>
                            <option>2:10 To 1:20</option>
                            <option>1:20 To 2:30</option>
                            <option>2:30 To 2:40</option>
                            <option>2:40 To 2:50</option>
                            <option>2:50 To 3:00</option>

                        </select>
                        <small>Slot starts at 9 AM and end 3 PM .</small>

                    </div>
                </div> -->

                <div class="text-center pt-10">
                    <button class="py-2 px-10 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3" type="submit" @click="customSubmit"> Book Now </button>

                    <button class="py-2 px-10 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3" type="reset"> Reset </button>

                </div>
            </table>
        </form>
        <br>
        <table class="list">
            <h1 class="text-teal-900 text-xl font-bold pt-1"> Booked slots</h1>
            <tr>
                <th class="px-4 border-black rounded-lg border-2">Id</th>
                <th class="px-4 border-black rounded-lg border-2">Name</th>
                <th class="px-4 border-black rounded-lg border-2"> Phone Number</th>
                <th class="px-4 border-black rounded-lg border-2">Date</th>
                <th class="px-4 border-black rounded-lg border-2"> time</th>

                <th class="px-4 border-black rounded-lg border-2">Action</th>
            </tr>

            <tr v-for="(item, i) in myarr" :key="item">
                <td class="px-4 border-black rounded-lg border-2">{{item.id = i+1}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.firstname}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.number}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.date}}</td>

                <td class="px-4 border-black rounded-lg border-2">{{item.time}}</td>

                <td class="px-4 border-black rounded-lg border-2">
                    <button class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md " type="delete" @click="customDelete(i)"> Slot Delete </button>
                    <button class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md" type="edit" @click="customEdit(i)"> Edit Details </button>

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
            indexEdit: -1,
            myarr: [],
            slot: 'time',

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

            this.isEdit = true;
            this.indexEdit = index;

        }
    }
}
</script>
