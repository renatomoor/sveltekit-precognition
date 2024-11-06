<script lang="ts">
    import {Button} from "$lib/components/ui/button";
    import * as Form from "$lib/components/form";
    import * as Card from "$lib/components/ui/card";
    import { useForm, client } from "$lib/precognition/packages/svelte";

    const axiosClient = client.axios();

    // add credentials to the request
    axiosClient.defaults.withCredentials = true;
    axiosClient.defaults.withXSRFToken = true;
    axiosClient.defaults.baseURL = import.meta.env.VITE_API_URL;

    let form = useForm('post', 'register', {
        name: '',
        email: '',
        password: '',
        password_confirmation: '',
    })

    $effect(() => {
        axiosClient.get('sanctum/csrf-cookie');
    })

    async function handleSubmit() {
        await form.submit()
    }
</script>

<!-- Registration Form -->

<Card.Root class="w-[350px]">
    <Card.Header>
        <Card.Title class="text-xl">
            Reactive values
        </Card.Title>
        <Card.Content class="grid gap-2">
            <span>Validating: {form.validating}</span>
            <span>Processing: {form.processing}</span>
            <span>hasErrors: {form.hasErrors}</span>
        </Card.Content>
    </Card.Header>
</Card.Root>

<Card.Root class="w-[450px] mt-4">
    <Card.Header>
        <Card.Title class="text-xl">
            Login
        </Card.Title>
        <Card.Description>
            Enter your information to create an account
        </Card.Description>

    </Card.Header>
    <Card.Content>
        <Form.Group
            class="grid gap-6"
        >
            <div class="grid gap-2 border border-rounded border-gray-200 p-3 rounded-xl">
                <Form.InputField
                    bind:value={form.data.name}
                    error={form.errors.name}
                    label="Name"
                    name="name"
                    on:change={() => form.validate('name')}
                    placeholder="Name"
                    required
                    type="text"
                />
                <div class="flex gap-2">
                   <span class="text-xs bg-gray-100/50 p-2 rounded">
                        Valid: {form.valid('name')}
                    </span>
                    <span class="text-xs bg-gray-100/50 p-2 rounded">
                        Invalid: {form.invalid('name')}
                    </span>
                    <span class="text-xs bg-gray-100/50 p-2 rounded">
                        Touched: {form.touched('name')}
                    </span>
                </div>

                <Button on:click={() => form.touch('name')} variant="secondary"> Touch</Button>
                <Button on:click={() => form.setErrors({name: 'New error'})} variant="secondary"> Set Error</Button>
                <Button on:click={() => form.forgetError('name')} variant="secondary"> Forget Error</Button>
            </div>


            <Form.InputField
                bind:value={form.data.email}
                error={form.errors.email}
                label="Email"
                on:change={() => form.validate('email')}
                placeholder="Email"
                required
                type="email"
            />

            <Form.InputField
                bind:value={form.data.password}
                error={form.errors.password}
                label="Password"
                placeholder="Password"
                required
                type="password"
            />

            <Form.InputField
                bind:value={form.data.password_confirmation}
                error={form.errors.password_confirmation}
                label="Confirm Password"
                on:change={() => form.validate('password_confirmation') && form.validate('password')}
                placeholder="Confirm Password"
                required
                type="password"
            />
        </Form.Group>
    </Card.Content>

    <Card.Footer class="flex justify-end items-center gap-6">
        <div class="text-center text-sm">
            <a class="underline" href="/login"> Already registered? </a>
        </div>

        <Button on:click={() => form.reset()} type="submit">Reset</Button>
        <Button on:click={handleSubmit} type="submit">Register</Button>
    </Card.Footer>
</Card.Root>

