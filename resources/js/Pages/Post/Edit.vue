<template>

    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Edit
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <div>
                                <label for="category_id">Category</label>
                                <input type="number" v-model="form.category_id" class="
                                        w-full
                                        px-4
                                        py-2
                                        mt-2
                                        border
                                        rounded-md
                                        focus:outline-none
                                        focus:ring-1
                                        focus:ring-blue-600
                                    " />
                                <div class="bg-red-100 my-3 border border-red-400 text-red-700 px-4 py-3 rounded relative"
                                    role="alert" v-if="errors.category_id">
                                    <strong class="font-bold">Category is not selected</strong>
                                </div>
                            </div>
                            <div>
                                <label for="title">Title</label>
                                <input type="text" v-model="form.title" class="
                                        w-full
                                        px-4
                                        py-2
                                        mt-2
                                        border
                                        rounded-md
                                        focus:outline-none
                                        focus:ring-1
                                        focus:ring-blue-600
                                    " />
                                <div class="bg-red-100 my-3 border border-red-400 text-red-700 px-4 py-3 rounded relative"
                                    role="alert" v-if="errors.title">
                                    <strong class="font-bold">{{ errors.title }}</strong>
                                </div>
                            </div>
                            <div>
                                <label for="title">Description</label>
                                <textarea name="description" type="text" v-model="form.description" class="
                                        w-full
                                        px-4
                                        py-2
                                        mt-2
                                        border
                                        rounded-md
                                        focus:outline-none
                                        focus:ring-1
                                        focus:ring-blue-600
                                    ">
                                </textarea>
                                <div class="bg-red-100 my-3 border border-red-400 text-red-700 px-4 py-3 rounded relative"
                                    role="alert" v-if="errors.description">
                                    <strong class="font-bold">{{ errors.description }}</strong>
                                </div>
                            </div>

                            <!-- submit -->
                            <div class="flex items-center mt-4">
                                <button class="
                                        px-6
                                        py-2
                                        text-white
                                        bg-gray-900
                                        rounded
                                    ">
                                    Save
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script>
import AuthenticatedLayout from "@/Layouts/Authenticated.vue";
import { Head } from "@inertiajs/inertia-vue3";
import { useForm } from "@inertiajs/inertia-vue3";
export default {
    components: {
        AuthenticatedLayout,
        Head,
    },
    setup(props) {
        const form = useForm({
            title: props.post.title,
            category_id: props.post.category_id,
            description: props.post.description,
        });

        return { form };
    },
    props: {
        post: Object,
        errors: Object
    },
    methods: {
        submit() {
            this.form.put(route("posts.update", this.post.id));
        },
    },
};
</script>