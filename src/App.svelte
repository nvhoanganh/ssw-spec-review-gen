<script>
  import Form from "./Form.svelte";
  // set default value for the form
  let value = {
    project: "Spec Review Generator",
    productOwner: {
      name: "Adam Cogan",
      title: "CEO",
      mobile: "+61 111 222 333",
      email: "adamcogan@ssw.com.au"
    },
    techLead: {
      name: "Anthony Nguyen",
      title: "Solution Architect",
      mobile: "+61 410 000 111",
      email: "anthonynguyen@ssw.com.au"
    },
    stateManager: {
      name: "Michael Smedley",
      title: "Vic State Manager",
      mobile: "+61 432 333 222",
      email: "michaelsmedley@ssw.com.au"
    },
    ui_areas: ["Login and Sign up page", "Home page", "Report", "Checkout"],
    outscope: ["Payment gateway", "Support after deployment"],
    tasks: [
      {
        name: "Initial setup",
        est: 8,
        mvp: true
      },
      {
        name: "Authentication with Google",
        est: 4,
        mvp: false
      },
      {
        name: "CI/CD setup",
        est: 16,
        mvp: true
      }
    ],
    avgRate: 1300,
    avgRateDiscounted: 1285
  };
  let name = "Northwind Trader";

  const downloadTemplate = () =>
    (window.location.href =
      "https://us-central1-python-func-export-template.cloudfunctions.net/template");

  const handleSubmit = () => {
    const totalHours = value.tasks
      .map(x => x.est)
      .reduce((current, pre) => current + pre, 0);

    const d = {
      author: {
        title: value.techLead.title,
        name: value.techLead.name
      },
      customer: {
        title: value.productOwner.title,
        name: value.productOwner.name
      },
      project: value.project,
      title: `${name} - ${value.project} Specifications Review`,
      parties: [
        {
          name: value.productOwner.name,
          company: name,
          role: value.productOwner.title,
          contact: {
            mobile: value.productOwner.mobile,
            email: value.productOwner.email
          }
        },
        {
          name: value.techLead.name,
          company: "SSW",
          role: value.techLead.title,
          contact: {
            mobile: value.techLead.mobile,
            email: value.techLead.email
          }
        },
        {
          name: value.stateManager.name,
          company: "SSW",
          role: value.stateManager.title,
          contact: {
            mobile: value.stateManager.mobile,
            email: value.stateManager.email
          }
        }
      ],
      ui_areas: value.ui_areas,
      has_more: value.has_more,
      outscope: value.outscope,
      total: totalHours + " h",
      std: `$ ${new Intl.NumberFormat("en-AU").format(
        totalHours * value.avgRate
      )}`,
      pre: `$ ${new Intl.NumberFormat("en-AU").format(
        totalHours * value.avgRateDiscounted
      )}`,
      tasks: value.tasks
        .filter(x => x.name.trim())
        .map(x => ({
          name: x.name,
          est: `${x.est} h`,
          std: `$${x.est * value.avgRate}`,
          pre: `$${x.est * value.avgRateDiscounted}`,
          ...(x.mvp && { bg: "42f557" }),
          ...(x.mvp && { mvp: "Y" })
        }))
    };
    console.log("submitted ->", d);
    window.location.href =
      "https://us-central1-python-func-export-template.cloudfunctions.net/json2docx?data=" +
      JSON.stringify(d);
  };
</script>

<style>

</style>

<main>
  <div class="container mx-2 md:mx-auto">
    <div class="text-4xl text-red-700 mx-auto mt-3 mb-8">
      SSW Specification Review - {name}
    </div>
    <p class="my-4">
      <a
        href="https://us-central1-python-func-export-template.cloudfunctions.net/template"
        class="text-blue-400 underline">
        View Template
      </a>
    </p>
    <Form
      bind:name
      bind:value
      on:submit={handleSubmit}
      on:downloadTemplate={downloadTemplate} />
  </div>
</main>
