# Kubernetes Example Operator

This repository contains a kubebuilder(v2)-generated Kubernetes operator. 

It is a feasibility research for using kind to support e2e tests for kubebuilder(v2)-generated Kubernetes operators.

The CRD of the operator is simple:

```go
// ApplicationSpec defines the desired state of Application
type ApplicationSpec struct {
	// INSERT ADDITIONAL SPEC FIELDS - desired state of cluster
	// Important: Run "make" to regenerate code after modifying this file
}

// ApplicationStatus defines the observed state of Application
type ApplicationStatus struct {
	// INSERT ADDITIONAL STATUS FIELD - define observed state of cluster
	// Important: Run "make" to regenerate code after modifying this file
}

// +kubebuilder:object:root=true

// Application is the Schema for the applications API
type Application struct {
	metav1.TypeMeta   `json:",inline"`
	metav1.ObjectMeta `json:"metadata,omitempty"`

	Spec   ApplicationSpec   `json:"spec,omitempty"`
	Status ApplicationStatus `json:"status,omitempty"`
}
```

The operator creates a nginx deployment for the application.

## Run E2E Tests with Kind

```bash
kind create cluster
export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"
make test
kind delete cluster
```
